## Chapter 3 Cheatsheet: FastAPI + Pydantic

### HTTP Methods & Idempotency
| Method | Idempotent? | Typical Use |
|---|---|---|
| GET | Yes | Read resource |
| POST | No | Create resource |
| PUT | Yes | Full replace |
| PATCH | No (usually) | Partial update |
| DELETE | Yes | Remove resource |

### Key Status Codes
| Code | Meaning | When |
|---|---|---|
| 200 | OK | Successful GET/PUT/generic |
| 201 | Created | Successful POST (new resource) |
| 204 | No Content | Successful DELETE, empty body |
| 400 | Bad Request | Manually raised HTTPException |
| 401 | Unauthorized | Missing/invalid auth |
| 403 | Forbidden | Authenticated but not allowed |
| 404 | Not Found | Resource doesn't exist |
| 422 | Unprocessable Entity | **Default** Pydantic validation failure |
| 500 | Internal Server Error | Unhandled server exception |

### def vs async def
| Type | Runs on | Blocking call effect |
|---|---|---|
| `def` | External threadpool (auto) | Safe, doesn't block event loop |
| `async def` | Event loop directly | Blocking call freezes ALL requests |

### Dependency Injection Pattern (DB session)
```python
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.get("/items")
def read_items(db: Session = Depends(get_db)):
    ...
```

### Pydantic Model Essentials
```python
from pydantic import BaseModel, Field

class UserIn(BaseModel):
    name: str = Field(max_length=50)
    age: int = Field(gt=0, le=120)

class UserOut(BaseModel):
    name: str
    age: int
    # hashed_password excluded on purpose
```
Use `response_model=UserOut` on the route to filter output fields (hide secrets).

### Auth Comparison
| Method | Stateless? | Carries Claims/Expiry? | Best For |
|---|---|---|
| API Key | Yes | No | Simple service auth |
| JWT | Yes | Yes | Stateless service-to-service / user sessions |
| Session Cookie | No | N/A | Server-rendered web apps |

### Swagger/OpenAPI
- `/docs` → Swagger UI (interactive)
- `/redoc` → ReDoc (read-only)
- Auto-generated from route type hints + Pydantic models — no manual spec needed.

### Run Command
```bash
uvicorn main:app --reload
```
`--reload` = dev only, never in production.

### Microservices Communication
| Pattern | Coupling | Failure Behavior |
|---|---|---|
| Sync (REST/gRPC) | Tight | Caller blocks/fails if callee down |
| Async (Message Queue) | Loose | Messages queue until consumer available |
