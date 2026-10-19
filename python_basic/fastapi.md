# FastAPI 完整学习指南：从入门到精通

> 🚀 最现代、最快速的 Python Web 框架，构建高性能 API 的必备工具

## 📚 完整目录

### 基础篇
1. [FastAPI 基础概念](#第一部分-fastapi-基础概念)
2. [快速开始](#第二部分快速开始)
3. [路径参数和查询参数](#第三部分路径参数和查询参数)
4. [请求体和数据验证](#第四部分请求体和数据验证)
5. [响应模型和序列化](#第五部分响应模型和序列化)

### 进阶篇
6. [错误处理和异常](#第六部分错误处理和异常)
7. [依赖注入系统](#第七部分依赖注入系统)
8. [中间件和 CORS](#第八部分中间件和-cors)
9. [静态文件和模板](#第九部分静态文件和模板)
10. [WebSocket 支持](#第十部分-websocket-支持)

### 高级篇
11. [后台任务](#第十一部分后台任务)
12. [数据库集成](#第十二部分数据库集成)
13. [用户认证和授权](#第十三部分用户认证和授权)
14. [测试](#第十四部分测试)
15. [部署和生产环境](#第十五部分部署和生产环境)
16. [最佳实践和项目实战](#第十六部分最佳实践和项目实战)

---

## 第一部分：FastAPI 基础概念

### 1.1 什么是 FastAPI？

**FastAPI** 是一个现代、高性能的 Python Web 框架，用于构建 API。

**核心特点：**
- 🚀 **快速**：基于 Starlette 和 Pydantic，性能媲美 Node.js 和 Go
- 🎯 **类型安全**：充分利用 Python 类型提示，自动数据验证
- 📝 **自动生成文档**：内置 Swagger UI 和 ReDoc
- 🔧 **IDE 友好**：优秀的自动补全和类型检查
- ✅ **生产就绪**：已被众多公司用于生产环境

### 1.2 为什么选择 FastAPI？

| 特性 | FastAPI | Flask | Django REST |
|------|---------|-------|-------------|
| 性能 | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ |
| 类型安全 | ✅ 自动 | ❌ 手动 | ⚠️ 部分 |
| 自动文档 | ✅ 内置 | ❌ 需插件 | ⚠️ 需配置 |
| 异步支持 | ✅ 原生 | ⚠️ 有限 | ⚠️ 有限 |
| 学习曲线 | 平缓 | 平缓 | 陡峭 |

### 1.3 安装

```bash
# 基础安装
pip install fastapi

# 生产环境（包含 UVicorn）
pip install "fastapi[all]"

# 或分别安装
pip install fastapi uvicorn[standard]

# 开发依赖
pip install python-multipart httpx pytest pytest-asyncio
```

### 1.4 核心依赖

```bash
# 核心库
fastapi          # Web 框架
uvicorn          # ASGI 服务器
pydantic         # 数据验证

# 常用扩展
python-multipart # 表单数据处理
httpx            # HTTP 客户端（测试用）
sqlalchemy       # ORM
alembic          # 数据库迁移
python-jose      # JWT 处理
passlib          # 密码哈希
bcrypt           # 密码加密
aiofiles         # 异步文件操作
```

---

## 第二部分：快速开始

### 2.1 第一个 FastAPI 应用

```python
from fastapi import FastAPI

app = FastAPI(
    title="我的 API",
    description="这是一个示例 API",
    version="1.0.0",
    docs_url="/docs",      # Swagger UI
    redoc_url="/redoc",    # ReDoc
    openapi_url="/openapi.json"
)

@app.get("/")
async def root():
    return {"message": "Hello World"}

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}

# 运行：uvicorn main:app --reload
```

**运行应用：**
```bash
# 开发模式（自动重载）
uvicorn main:app --reload

# 生产模式
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4

# 指定端口
uvicorn main:app --reload --port 5000
```

**访问文档：**
- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc
- OpenAPI JSON: http://localhost:8000/openapi.json

### 2.2 HTTP 方法装饰器

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items")     # GET 请求
async def get_items():
    return ["item1", "item2"]

@app.post("/items")    # POST 请求
async def create_item():
    return {"status": "created"}

@app.put("/items/1")   # PUT 请求
async def update_item():
    return {"status": "updated"}

@app.delete("/items/1") # DELETE 请求
async def delete_item():
    return {"status": "deleted"}

@app.patch("/items/1")  # PATCH 请求
async def patch_item():
    return {"status": "patched"}

@app.options("/items")  # OPTIONS 请求
async def options_item():
    return {"status": "options"}
```

### 2.3 Async 和 Await

```python
import asyncio
from fastapi import FastAPI

app = FastAPI()

# 异步端点（推荐）
@app.get("/async")
async def async_endpoint():
    await asyncio.sleep(1)  # 非阻塞
    return {"type": "async"}

# 同步端点（FastAPI 会在后台线程池运行）
@app.get("/sync")
def sync_endpoint():
    time.sleep(1)  # 阻塞
    return {"type": "sync"}

# 最佳实践：IO 操作使用 async
@app.get("/users/{user_id}")
async def get_user(user_id: int):
    # 数据库查询、HTTP 请求等 IO 操作
    user = await db.query(User).get(user_id)
    return user
```


---

## 第三部分：路径参数和查询参数

### 3.1 路径参数（Path Parameters）

```python
from fastapi import FastAPI, Path

app = FastAPI()

# 基本路径参数
@app.get("/users/{user_id}")
async def get_user(user_id: int):  # 自动转换为 int
    return {"user_id": user_id}

# 路径参数验证
@app.get("/items/{item_id}")
async def get_item(
    item_id: int = Path(..., title="物品 ID", description="物品的唯一标识符", ge=1, le=1000)
):
    return {"item_id": item_id}

# 字符串路径参数
@app.get("/articles/{article_slug}")
async def get_article(article_slug: str):
    return {"slug": article_slug}

# 包含路径分隔符的路径参数
@app.get("/files/{file_path:path}")
async def read_file(file_path: str):
    return {"file_path": file_path}
```

### 3.2 查询参数（Query Parameters）

```python
from fastapi import FastAPI, Query
from typing import Optional, List

app = FastAPI()

# 基本查询参数
@app.get("/items")
async def list_items(
    skip: int = 0,           # 默认值
    limit: int = 10,         # 默认值
    search: Optional[str] = None  # 可选参数
):
    return {
        "skip": skip,
        "limit": limit,
        "search": search
    }

# 查询参数验证
@app.get("/products")
async def list_products(
    page: int = Query(1, ge=1, description="页码"),
    size: int = Query(10, ge=1, le=100, description="每页数量"),
    sort: str = Query("created_at", regex="^(created_at|price|name)$"),
    order: str = Query("desc", regex="^(asc|desc)$")
):
    return {
        "page": page,
        "size": size,
        "sort": sort,
        "order": order
    }

# 多个相同参数的查询
@app.get("/tags")
async def get_by_tags(tags: List[str] = Query(...)):
    # GET /tags?tags=python&tags=fastapi
    return {"tags": tags}

# 必需 vs 可选
@app.get("/search")
async def search(
    q: str = Query(..., min_length=3),  # 必需参数
    category: Optional[str] = Query(None, title="分类")  # 可选参数
):
    return {"q": q, "category": category}
```

### 3.3 路径参数 vs 查询参数

```python
# URL: /users/123/items?skip=0&limit=10

@app.get("/users/{user_id}/items")
async def get_user_items(
    user_id: int,              # 路径参数（必需）
    skip: int = 0,             # 查询参数（可选）
    limit: int = 10            # 查询参数（可选）
):
    return {
        "user_id": user_id,
        "skip": skip,
        "limit": limit
    }
```

---

## 第四部分：请求体和数据验证

### 4.1 Pydantic 模型作为请求体

```python
from fastapi import FastAPI
from pydantic import BaseModel, Field, EmailStr
from typing import Optional, List
from datetime import datetime

app = FastAPI()

class UserCreate(BaseModel):
    username: str = Field(..., min_length=3, max_length=50)
    email: EmailStr
    password: str = Field(..., min_length=8)
    full_name: Optional[str] = None
    tags: List[str] = []

@app.post("/users")
async def create_user(user: UserCreate):
    return {
        "username": user.username,
        "email": user.email,
        "created_at": datetime.now()
    }
```

### 4.2 字段验证和约束

```python
from pydantic import BaseModel, Field, validator, HttpUrl
import re

class ProductCreate(BaseModel):
    name: str = Field(
        ...,
        min_length=1,
        max_length=100,
        description="产品名称",
        example="iPhone 15"
    )
    price: float = Field(
        ...,
        gt=0,
        le=100000,
        description="价格"
    )
    stock: int = Field(
        default=0,
        ge=0,
        description="库存数量"
    )
    website: Optional[HttpUrl] = None
    
    # 自定义验证器
    @validator('name')
    def validate_name(cls, v):
        if not re.match(r'^[\w\s-]+$', v):
            raise ValueError('名称包含非法字符')
        return v.title()
    
    @validator('price')
    def validate_price(cls, v):
        if v < 0:
            raise ValueError('价格不能为负数')
        return round(v, 2)

class UserRegister(BaseModel):
    email: EmailStr
    password: str = Field(..., min_length=8)
    confirm_password: str
    
    @validator('confirm_password')
    def passwords_match(cls, v, values):
        if 'password' in values and v != values['password']:
            raise ValueError('两次密码不一致')
        return v
```

### 4.3 可选的请求体字段

```python
class UserUpdate(BaseModel):
    username: Optional[str] = Field(None, min_length=3)
    email: Optional[EmailStr] = None
    full_name: Optional[str] = None
    is_active: Optional[bool] = None
    
    class Config:
        validate_assignment = True

@app.patch("/users/{user_id}")
async def update_user(user_id: int, user: UserUpdate):
    # 只更新提供的字段
    update_data = user.dict(exclude_unset=True)
    return {"updated": update_data}
```

### 4.4 嵌套模型

```python
class Address(BaseModel):
    street: str
    city: str
    province: str
    zip_code: str

class UserProfile(BaseModel):
    bio: str
    avatar_url: Optional[str] = None
    social_links: dict = {}

class UserCreateAdvanced(BaseModel):
    username: str
    email: EmailStr
    profile: UserProfile
    address: Address
    tags: List[str] = []

@app.post("/users/advanced")
async def create_user_advanced(user: UserCreateAdvanced):
    return {
        "username": user.username,
        "city": user.address.city,
        "bio": user.profile.bio
    }
```


---

## 第五部分：响应模型和序列化

### 响应模型 (Response Model)

```python
from fastapi import FastAPI
from pydantic import BaseModel
from datetime import datetime

app = FastAPI()

class UserCreate(BaseModel):
    username: str
    email: str

class UserResponse(BaseModel):
    id: int
    username: str
    created_at: datetime
    
    class Config:
        from_attributes = True

@app.post('/users', response_model=UserResponse)
async def create_user(user: UserCreate):
    return {'id': 1, 'username': user.username, 'created_at': datetime.now()}
```

### 过滤响应数据

```python
# 排除敏感字段
@app.get('/users/{user_id}', response_model_exclude={'password'})
async def get_user(user_id: int):
    return user_data
```

---

## 第六部分：错误处理和异常

### HTTPException

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

@app.get('/items/{item_id}')
async def get_item(item_id: int):
    if item_id not in items_db:
        raise HTTPException(status_code=404, detail='Item not found')
    return {'item': items_db[item_id]}
```

### 自定义异常处理器

```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse

class CustomException(Exception):
    pass

@app.exception_handler(CustomException)
async def handle_custom(request: Request, exc: CustomException):
    return JSONResponse(status_code=400, content={'error': str(exc)})
```

---

## 第七部分：依赖注入系统

### 基础依赖

```python
from fastapi import FastAPI, Depends

app = FastAPI()

async def common_params(q=None, skip=0, limit=100):
    return {'q': q, 'skip': skip, 'limit': limit}

@app.get('/items')
async def read_items(commons=Depends(common_params)):
    return commons
```

### 数据库依赖

```python
from sqlalchemy.orm import Session

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.get('/users/{user_id}')
async def get_user(user_id: int, db: Session = Depends(get_db)):
    return db.query(User).filter(User.id == user_id).first()
```

---

## 第八部分：中间件和 CORS

### 添加中间件

```python
from fastapi import FastAPI, Request
import time

app = FastAPI()

@app.middleware('http')
async def add_process_time(request: Request, call_next):
    start = time.time()
    response = await call_next(request)
    response.headers['X-Process-Time'] = str(time.time() - start)
    return response
```

### CORS

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=['http://localhost:3000'],
    allow_credentials=True,
    allow_methods=['*'],
    allow_headers=['*']
)
```

---

## 第九部分：WebSocket 支持

```python
from fastapi import FastAPI, WebSocket

app = FastAPI()

@app.websocket('/ws')
async def websocket_endpoint(websocket: WebSocket):
    await websocket.accept()
    while True:
        data = await websocket.receive_text()
        await websocket.send_text(f'Message: {data}')
```

---

## 第十部分：后台任务

```python
from fastapi import FastAPI, BackgroundTasks

app = FastAPI()

def send_email(email: str, message: str):
    print(f'Sending to {email}: {message}')

@app.post('/send-email')
async def send_email_endpoint(email: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(send_email, email, 'Hello!')
    return {'message': 'Email queued'}
```

---

## 第十一部分：数据库集成 (SQLAlchemy)

### 数据库设置

```python
# database.py
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

engine = create_engine('sqlite:///./test.db')
SessionLocal = sessionmaker(bind=engine)
Base = declarative_base()

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

### 定义模型

```python
# models.py
from sqlalchemy import Column, Integer, String

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    email = Column(String, unique=True)
    username = Column(String)
```

### Pydantic Schemas

```python
# schemas.py
from pydantic import BaseModel

class UserCreate(BaseModel):
    email: str
    username: str

class UserResponse(BaseModel):
    id: int
    email: str
    username: str
    class Config:
        from_attributes = True
```

---

## 第十二部分：用户认证和授权 (JWT)

```python
from datetime import datetime, timedelta
from jose import jwt
from passlib.context import CryptContext

SECRET_KEY = 'your-secret-key'
ALGORITHM = 'HS256'

pwd_context = CryptContext(schemes=['bcrypt'])

def create_access_token(data: dict):
    expire = datetime.utcnow() + timedelta(minutes=30)
    data.update({'exp': expire})
    return jwt.encode(data, SECRET_KEY, algorithm=ALGORITHM)
```

---

## 第十三部分：测试

```python
from fastapi.testclient import TestClient
from main import app

client = TestClient(app)

def test_read_main():
    response = client.get('/')
    assert response.status_code == 200
    assert response.json() == {'message': 'Hello World'}
```

---

## 第十四部分：部署和生产环境

### Docker 部署

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Gunicorn + Uvicorn

```bash
gunicorn main:app --workers 4 --worker-class uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000
```

---

## 第十五部分：最佳实践

### 项目结构

```
my_project/
├── app/
│   ├── main.py
│   ├── api/
│   │   ├── users.py
│   │   └── items.py
│   ├── models/
│   ├── schemas/
│   └── crud/
├── tests/
└── requirements.txt
```

### APIRouter 组织路由

```python
# api/users.py
from fastapi import APIRouter

router = APIRouter(prefix='/users', tags=['users'])

@router.get('/')
def get_users():
    return []

# main.py
from fastapi import FastAPI
from api import users

app = FastAPI()
app.include_router(users.router)
```

### 性能优化

1. 使用异步 IO
2. 数据库连接池
3. Redis 缓存
4. 分页查询
5. 数据库索引
6. GZip 压缩

### 安全最佳实践

1. HTTPS 生产环境
2. 严格 CORS 配置
3. 输入验证
4. SQL 注入防护
5. 速率限制
6. 日志记录

---

## 总结

恭喜你完成了 FastAPI 的完整学习！

### 核心要点

1. FastAPI 是现代高性能 Python Web 框架
2. 类型安全，自动数据验证
3. 内置 Swagger UI 和 ReDoc
4. 强大的依赖注入系统
5. 原生 async/await 支持
6. 与 SQLAlchemy 完美配合
7. 支持 OAuth2 和 JWT
8. 易于测试和部署

### 资源

- 官方文档：https://fastapi.tiangolo.com
- GitHub: https://github.com/tiangolo/fastapi
- Awesome FastAPI: https://github.com/mjhea0/awesome-fastapi

祝你学习愉快！🎉
