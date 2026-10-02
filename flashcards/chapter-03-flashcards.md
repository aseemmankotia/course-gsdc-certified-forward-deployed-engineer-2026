## Chapter 3: Building APIs with FastAPI and Pydantic — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Default HTTP status code FastAPI returns for Pydantic validation errors? | 422 Unprocessable Entity. Exam tip: not 400 — 400 is reserved for manually raised HTTPException errors. |
| 2 | HTTP status code for successful resource creation via POST? | 201 Created. Should include a Location header pointing to the new resource. Exam tip: don't default to 200 for creation endpoints. |
| 3 | HTTP status code for successful DELETE with no response body? | 204 No Content. Exam tip: the response body must be empty when returning 204. |
| 4 | def vs async def in FastAPI — which runs in a threadpool automatically? | Regular 'def' endpoints run in an external threadpool automatically. 'async def' endpoints run directly on the event loop — a blocking call inside them freezes all concurrency. |
| 5 | FastAPI dependency pattern for a DB session with guaranteed cleanup | def get_db():     db = SessionLocal()     try:         yield db     finally:         db.close() Inject via Depends(get_db). Exam tip: yield-based dependencies act like context managers. |
| 6 | Pydantic v2 syntax to enforce max length 50 on a string field | from pydantic import Field name: str = Field(max_length=50) Exam tip: Field() adds constraints beyond basic type checking. |
| 7 | How to hide sensitive fields (e.g., password hash) from API responses? | Define a response_model Pydantic schema that excludes the field. Exam tip: response_model filters output regardless of what the endpoint function returns internally. |
| 8 | PUT vs PATCH — which is idempotent? | PUT is idempotent (full resource replacement, same end state on repeat). PATCH is NOT guaranteed idempotent (partial update). Exam tip: GET and DELETE are also idempotent. |
| 9 | JWT vs API key — best for stateless service-to-service auth? | JWT: self-contained, carries claims/expiration, no server-side session needed. API key: simpler but has no built-in expiry or claims. Exam tip: choose JWT when statelessness is emphasized. |
| 10 | FastAPI auto-generated interactive docs URL paths | /docs = Swagger UI, /redoc = ReDoc. Generated automatically from Pydantic models + type hints. Exam tip: no manual OpenAPI spec writing required by default. |
| 11 | Command to run a FastAPI app locally with auto-reload | uvicorn main:app --reload. Exam tip: --reload is for development only — never use in production. |
| 12 | Microservices inter-service communication: sync vs async pattern | Sync: REST/HTTP or gRPC — waits for response, tighter coupling. Async: message queue (e.g., Kafka/RabbitMQ) — decoupled, better resilience/scaling. Exam tip: pick async when a service must stay available even if a dependency is down. |
