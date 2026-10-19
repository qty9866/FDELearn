# Python 异步编程完整指南：从同步到 Celery

> 💡 彻底搞懂并发编程：threading、multiprocessing、asyncio、消息队列、Celery

---

## 📚 完整目录

### 基础篇 (1-8)
1. 为什么需要异步？同步 vs 异步
2. 并发编程核心概念
3. threading 多线程详解
4. multiprocessing 多进程详解
5. GIL 全局解释器锁
6. 何时用线程？何时用进程？
7. 协程与 async/await 基础
8. asyncio 事件循环原理

### 进阶篇 (9-16)
9. async/await 深入理解
10. asyncio 任务与调度
11. 异步上下文管理器
12. 异步迭代器
13. concurrent.futures 统一接口
14. 线程池与进程池
15. 异步 HTTP 请求 (aiohttp)
16. 异步数据库操作

### 消息队列篇 (17-22)
17. 消息队列基础概念
18. RabbitMQ 入门与实战
19. Redis 作为消息队列
20. Kafka 简介
21. 生产者 - 消费者模式
22. 消息确认与持久化

### Celery 实战篇 (23-30)
23. Celery 是什么？为什么需要它？
24. Celery 架构详解
25. 安装与配置
26. 第一个 Celery 任务
27. 任务路由与队列
28. 定时任务 (Celery Beat)
29. 任务监控与管理
30. Celery 最佳实践

### 综合实战篇 (31-35)
31. 异步 Web 爬虫
32. 实时数据处理管道
33. 后台任务处理系统
34. 微服务间通信
35. 性能优化与调试

---

## 第一部分：为什么需要异步？

### 同步编程的问题

```python
import time
import requests

def download_image(url, filename):
    print(f"开始下载 {filename}")
    response = requests.get(url)
    time.sleep(2)
    with open(filename, 'wb') as f:
        f.write(response.content)
    print(f"完成下载 {filename}")

urls = [f"http://example.com/img{i}.jpg" for i in range(5)]
start = time.time()
for i, url in enumerate(urls):
    download_image(url, f"img{i}.jpg")
end = time.time()

print(f"总耗时：{end - start:.2f}秒")  # 约 10 秒
```

**问题：** 
- ❌ CPU 等待 I/O 完成
- ❌ 资源利用率低
- ❌ 用户体验差
- ❌ 扩展性差

### 异步解决方案

```python
import asyncio
import aiohttp

async def download_image(session, url, filename):
    async with session.get(url) as response:
        await asyncio.sleep(2)
        content = await response.read()
        with open(filename, 'wb') as f:
            f.write(content)

async def main():
    urls = [f"http://example.com/img{i}.jpg" for i in range(5)]
    async with aiohttp.ClientSession() as session:
        tasks = [download_image(session, url, f"img{i}.jpg") 
                 for i, url in enumerate(urls)]
        await asyncio.gather(*tasks)

start = time.time()
asyncio.run(main())
end = time.time()
print(f"总耗时：{end - start:.2f}秒")  # 约 2 秒
```

**优势：**
- ✅ CPU 不等待，利用等待时间做其他事
- ✅ 资源利用率高
- ✅ 响应速度快
- ✅ 可扩展性强

### 性能对比

| 场景 | 同步 | 异步 | 提升 |
|------|------|------|------|
| 下载 5 张图片 | 10 秒 | 2 秒 | **5 倍** |
| 100 个 API 请求 | 100 秒 | 5 秒 | **20 倍** |

---

## 第二部分：并发方案对比

| 方案 | 适用场景 | 优点 | 缺点 |
|------|---------|------|------|
| **threading** | I/O 密集型 | 简单，共享内存 | GIL 限制 |
| **multiprocessing** | CPU 密集型 | 无 GIL，多核 | 内存开销大 |
| **asyncio** | I/O 密集型 | 高性能，轻量 | 学习曲线陡 |
| **Celery** | 分布式任务 | 跨机器，可靠 | 复杂，需中间件 |

---

## 第三部分：threading 多线程

### 基础用法

```python
import threading
import time

def worker(name, delay):
    for i in range(3):
        print(f"{name} 第 {i+1} 次")
        time.sleep(delay)

t1 = threading.Thread(target=worker, args=("A", 1))
t2 = threading.Thread(target=worker, args=("B", 1.5))
t1.start()
t2.start()
t1.join()
t2.join()
```

### Lock 同步

```python
lock = threading.Lock()
counter = 0

def increment():
    global counter
    for _ in range(100000):
        with lock:
            counter += 1
```

### ThreadLocal

```python
local_data = threading.local()

def worker(value):
    local_data.value = value
    print(f"{threading.current_thread().name}: {local_data.value}")
```

---

## 第四部分：multiprocessing 多进程

### 基础用法

```python
from multiprocessing import Process
import os

def worker(name):
    print(f"{name} PID: {os.getpid()}")
    time.sleep(2)

if __name__ == '__main__':
    p1 = Process(target=worker, args=("P1",))
    p2 = Process(target=worker, args=("P2",))
    p1.start()
    p2.start()
    p1.join()
    p2.join()
```

### Pool 进程池

```python
from multiprocessing import Pool

def square(x): return x * x

with Pool(4) as p:
    results = p.map(square, range(10))
```

### 进程间通信 Queue

```python
from multiprocessing import Process, Queue

def producer(q):
    for i in range(5):
        q.put(i)

def consumer(q):
    while True:
        item = q.get()
        print(f"消费：{item}")
```

---

## 第五部分：GIL 全局解释器锁

**GIL** 确保同一时刻只有一个线程执行 Python 字节码。

**绕过方法：**
1. 多进程 (`multiprocessing`)
2. C 扩展 (NumPy)
3. asyncio 协程

---

## 第六部分：选择指南

| 场景 | 推荐方案 |
|------|---------|
| CPU 密集型 | `multiprocessing` |
| I/O 密集型 | `threading` / `asyncio` |
| 共享状态 | `threading` + Lock |
| 隔离性高 | `multiprocessing` |
| 大量连接 | `asyncio` |
| 跨机器 | `Celery` |

---

## 第七部分：async/await 基础

```python
import asyncio

async def say():
    print("Hello")
    await asyncio.sleep(1)
    print("World")

asyncio.run(say())
```

---

## 第八部分：asyncio 事件循环

```python
async def work():
    await asyncio.sleep(1)
    return "done"

async def main():
    task = asyncio.create_task(work())
    result = await task
    print(result)

asyncio.run(main())
```

### 超时处理

```python
try:
    result = await asyncio.wait_for(long_task(), timeout=2.0)
except asyncio.TimeoutError:
    print("超时!")
```

---

（基础篇完，继续消息队列和 Celery...）

---

## 第九部分：消息队列基础概念

### 什么是消息队列？

**消息队列 (Message Queue)** 是一种进程间通信机制，用于在分布式系统中传递消息。

```
生产者 → [消息队列] → 消费者
```

### 为什么需要消息队列？

1. **解耦**：生产者和消费者不需要直接通信
2. **异步**：发送者不需要等待接收者处理
3. **削峰**：缓冲突发流量
4. **可靠**：消息持久化，不丢失

### 常见消息队列对比

| 消息队列 | 特点 | 适用场景 |
|---------|------|---------|
| **RabbitMQ** | AMQP 协议，功能完善 | 一般业务消息 |
| **Redis** | 简单，高性能 | 轻量级任务队列 |
| **Kafka** | 高吞吐，持久化 | 日志、大数据 |
| **RocketMQ** | 阿里出品，高可用 | 电商、金融 |

---

## 第十部分：RabbitMQ 入门

### 安装 RabbitMQ

```bash
# macOS
brew install rabbitmq
brew services start rabbitmq

# Docker
docker run -d --name rabbitmq \
  -p 5672:5672 -p 15672:15672 \
  rabbitmq:3-management
```

访问管理界面：http://localhost:15672 (guest/guest)

### Python 使用 pika

```python
import pika

# 连接
connection = pika.BlockingConnection(
    pika.ConnectionParameters('localhost')
)
channel = connection.channel()

# 声明队列
channel.queue_declare(queue='hello')

# 发送消息
channel.basic_publish(
    exchange='',
    routing_key='hello',
    body='Hello World!'
)

# 消费消息
def callback(ch, method, properties, body):
    print(f"收到消息：{body}")

channel.basic_consume(
    queue='hello',
    on_message_callback=callback,
    auto_ack=True
)

channel.start_consuming()
```

---

## 第十一部分：Redis 作为消息队列

### List 实现队列

```python
import redis
import json

r = redis.Redis(host='localhost', port=6379)

# 生产者
task = {'id': 1, 'name': 'process_image'}
r.lpush('task_queue', json.dumps(task))

# 消费者（阻塞式）
task = r.brpop('task_queue', timeout=5)
if task:
    data = json.loads(task[1])
    print(f"处理任务：{data}")
```

### Pub/Sub 发布订阅

```python
# 发布
r.publish('channel_name', 'message')

# 订阅
pubsub = r.pubsub()
pubsub.subscribe('channel_name')

for message in pubsub.listen():
    print(f"收到：{message['data']}")
```

---

## 第十二部分：Kafka 简介

```python
from kafka import KafkaProducer, KafkaConsumer
import json

# 生产者
producer = KafkaProducer(
    bootstrap_servers=['localhost:9092'],
    value_serializer=lambda v: json.dumps(v).encode('utf-8')
)
producer.send('my_topic', {'key': 'value'})

# 消费者
consumer = KafkaConsumer(
    'my_topic',
    bootstrap_servers=['localhost:9092'],
    value_deserializer=lambda m: json.loads(m.decode('utf-8'))
)

for message in consumer:
    print(f"收到：{message.value}")
```

---

## 第十三部分：Celery 是什么？

### 使用场景

- 用户注册后发送邮件（耗时）
- 上传视频需要转码（耗时）
- 定期生成报表（定时）

### Celery 架构

```
Web App → Broker (Redis) → Worker (Celery)
                     ↓
                Backend (存储结果)
```

**组件：**
1. **Broker**：消息中间件（Redis/RabbitMQ）
2. **Worker**：任务执行者
3. **Backend**：存储结果（可选）

---

## 第十四部分：Celery 安装与配置

### 安装

```bash
pip install celery redis
# 或
pip install celery[rabbitmq]
```

### 项目结构

```
myproject/
├── celery_app.py      # Celery 配置
├── tasks.py           # 任务定义
└── main.py            # 主程序
```

### 配置 celery_app.py

```python
from celery import Celery

app = Celery(
    'myapp',
    broker='redis://localhost:6379/0',
    backend='redis://localhost:6379/1'
)

app.conf.update(
    task_serializer='json',
    accept_content=['json'],
    result_serializer='json',
    timezone='Asia/Shanghai',
    enable_utc=True,
)
```

---

## 第十五部分：第一个 Celery 任务

### 定义任务 tasks.py

```python
from celery_app import app
import time

@app.task
def add(x, y):
    return x + y

@app.task
def send_email(to, subject, body):
    time.sleep(2)
    print(f"邮件已发送到 {to}")
    return "sent"
```

### 调用任务 main.py

```python
from tasks import add, send_email

# 同步调用
result = add(2, 3)
print(result)  # 5

# 异步调用（推荐）
result = add.delay(2, 3)
print(result.get())  # 5

# 带参数
send_email.delay(
    to='user@example.com',
    subject='欢迎',
    body='感谢注册！'
)
```

### 启动 Worker

```bash
# 终端 1：启动 worker
celery -A tasks worker --loglevel=info

# 终端 2：运行主程序
python main.py
```

---

## 第十六部分：任务路由与队列

### 多队列配置

```python
# celery_app.py
app.conf.task_routes = {
    'tasks.send_email': {'queue': 'email'},
    'tasks.process_video': {'queue': 'video'},
    'tasks.*': {'queue': 'default'},
}
```

### 指定队列发送

```python
send_email.apply_async(
    args=['user@example.com', '标题', '内容'],
    queue='email'
)

# 启动特定队列的 worker
celery -A tasks worker -Q email --loglevel=info
```

---

## 第十七部分：定时任务 Celery Beat

### 配置定时任务

```python
from celery.schedules import crontab

app.conf.beat_schedule = {
    # 每天凌晨 2 点
    'daily-report': {
        'task': 'tasks.generate_daily_report',
        'schedule': crontab(hour=2, minute=0),
    },
    
    # 每 5 分钟
    'check-status': {
        'task': 'tasks.check_system_status',
        'schedule': 300.0,
    },
    
    # 每周一上午 9 点
    'weekly-meeting': {
        'task': 'tasks.send_meeting_reminder',
        'schedule': crontab(hour=9, minute=0, day_of_week=1),
    },
}
```

### 启动 Beat

```bash
celery -A tasks beat --loglevel=info
```

---

## 第十八部分：任务监控与管理

### Flower 监控

```bash
pip install flower
celery -A tasks flower --port=5555
```

访问 http://localhost:5555 查看任务状态、Worker 状态、任务历史。

### 查询任务状态

```python
from celery.result import AsyncResult

result = AsyncResult('task-id-here', app=app)
print(result.status)   # PENDING, SUCCESS, FAILURE
print(result.result)   # 返回值
print(result.ready())  # 是否完成
```

### 撤销任务

```python
from celery.task.control import revoke
revoke('task-id-here', terminate=True)
```

---

## 第十九部分：Celery 最佳实践

### 1. 任务幂等性

```python
@app.task(bind=True, max_retries=3)
def process_payment(self, order_id):
    try:
        if is_processed(order_id):
            return "already processed"
        process(order_id)
    except Exception as exc:
        raise self.retry(exc=exc, countdown=60)
```

### 2. 任务超时

```python
@app.task(time_limit=300, soft_time_limit=240)
def long_running_task():
    pass
```

### 3. 错误处理

```python
@app.task(bind=True)
def risky_task(self, data):
    try:
        return process(data)
    except Exception as e:
        logger.error(f"任务失败：{e}")
        send_alert(str(e))
        raise self.retry(exc=e, max_retries=3)
```

### 4. 任务链

```python
from celery import chain, group

# 链式执行
job = chain(
    tasks.step1.s(),
    tasks.step2.s(),
    tasks.step3.s()
)
result = job.apply_async()

# 并行执行
group_job = group(tasks.task1.s(), tasks.task2.s())
results = group_job.apply_async()
```

---

## 第二十部分：综合实战

### 实战：后台任务系统

```python
# tasks.py
from celery_app import app

@app.task
def resize_image(image_path, size):
    from PIL import Image
    img = Image.open(image_path)
    img.resize(size).save(f"resized_{image_path}")
    return f"resized_{image_path}"

@app.task
def send_notification(user_id, message):
    # 发送通知
    pass

# main.py
from tasks import resize_image, send_notification

# 用户上传后异步处理
resize_image.delay('photo.jpg', (800, 600))
send_notification.delay(user_id=123, message="处理完成")
```

---

## 总结

### 知识体系

```
Python 并发编程
├── 多线程 (threading)
│   ├── Lock, Condition
│   └── ThreadLocal
├── 多进程 (multiprocessing)
│   ├── Process, Pool
│   └── Queue, Pipe
├── 协程 (asyncio)
│   ├── async/await
│   └── aiohttp
└── 分布式任务 (Celery)
    ├── Broker (Redis/RabbitMQ)
    ├── Worker
    └── Beat (定时)
```

### 选择决策树

```
需要并发？
├── CPU 密集型 → multiprocessing
├── I/O 密集型
│   ├── 少量连接 → threading
│   └── 大量连接 → asyncio
└── 跨机器/后台任务 → Celery
```

### 下一步学习

1. **深入 asyncio**：理解事件循环底层
2. **学习 FastAPI**：现代异步 Web 框架
3. **掌握 Docker**：容器化部署 Celery
4. **了解 Kubernetes**：大规模任务调度

---

## 参考资源

- [Python asyncio 文档](https://docs.python.org/3/library/asyncio.html)
- [Celery 官方文档](https://docs.celeryq.dev/)
- [RabbitMQ 教程](https://www.rabbitmq.com/getstarted.html)
- [Redis 文档](https://redis.io/documentation)

