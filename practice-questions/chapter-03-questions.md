## Chapter 3: Building APIs with FastAPI and Pydantic — Practice Questions

**Q1.** A FastAPI endpoint creates a new resource via POST /users. Which HTTP status code should be returned on success?

A) 200 OK
B) 201 Created
C) 204 No Content
D) 202 Accepted

<details>
<summary>Answer</summary>

**Correct: B**

201 Created is the REST-correct status for successful resource creation; the response should also include a Location header pointing to the new resource.

**Why the others are wrong:**
- 200 is a generic success code used for GET/PUT, not creation semantics.
- 204 signals no response body, typically used for successful DELETE.
- 202 signals the request was accepted for async/background processing, not immediate creation.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A developer defines an 'async def' FastAPI endpoint that directly calls a blocking synchronous function (e.g., a sync DB driver call) without offloading it. What happens?

A) The blocking call freezes the event loop, stalling all other concurrent requests
B) FastAPI automatically runs it in a threadpool
C) FastAPI raises a runtime error since sync calls aren't allowed
D) The call runs in parallel automatically via multiprocessing

<details>
<summary>Answer</summary>

**Correct: A**

async def routes execute directly on the single event loop; a blocking call inside them halts all concurrency until it completes.

**Why the others are wrong:**
- Automatic threadpool offloading only happens for regular 'def' endpoints, not 'async def' ones — this is the core exam gotcha.
- Python permits calling sync functions inside async functions syntactically; no error is raised.
- There is no automatic multiprocessing in FastAPI's request handling.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An internal microservice must authenticate short-lived, stateless requests from a trusted client with minimal server-side session storage. Which auth approach BEST fits?

A) Session cookies stored server-side
B) JWT bearer token validated on each request
C) Basic auth with credentials on every call
D) OAuth2 authorization code flow with browser redirect

<details>
<summary>Answer</summary>

**Correct: B**

JWT is stateless and self-contained, carrying claims and expiration without requiring server-side session storage — ideal for service-to-service auth.

**Why the others are wrong:**
- Session cookies require a server-side session store, violating the stateless requirement.
- Basic auth sends raw credentials every call and has no expiration or claims.
- Authorization code flow requires a user browser redirect, unsuitable for machine-to-machine calls.

</details>

---

**Q4.** A FastAPI route needs a database session opened before the request and reliably closed after, even if an exception occurs. Which FastAPI feature is the standard solution?

A) A global variable initialized at app startup
B) Middleware that manually manages connections per request
C) A decorator applied directly above the route function
D) Depends() with a generator function using yield

<details>
<summary>Answer</summary>

**Correct: D**

A yield-based dependency function acts like a context manager: code before yield runs on request start, code after yield (in try/finally) runs on cleanup, guaranteeing closure even on exceptions.

**Why the others are wrong:**
- A global session is not request-scoped and is unsafe under concurrency.
- Middleware could technically work but is not the standard exam-tested dependency pattern.
- A plain decorator has no built-in mechanism for post-request cleanup.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Why are Pydantic models used for FastAPI request bodies instead of manually parsing raw JSON dicts?

A) Pydantic validates types/constraints and auto-generates the OpenAPI schema
B) Pydantic automatically stores data in a database
C) Pydantic replaces the need for HTTP status codes
D) Pydantic encrypts request payloads by default

<details>
<summary>Answer</summary>

**Correct: A**

Pydantic enforces type validation and field constraints at the boundary and feeds FastAPI's automatic OpenAPI/Swagger documentation generation.

**Why the others are wrong:**
- Pydantic has no built-in database persistence capability.
- Status codes are unrelated to Pydantic's validation role.
- Pydantic performs no encryption by default.

</details>

---

**Q6.** A client sends a POST request with a JSON body missing a required Pydantic field. With no custom exception handling, what status code does FastAPI return by default?

A) 400 Bad Request
B) 500 Internal Server Error
C) 422 Unprocessable Entity
D) 409 Conflict

<details>
<summary>Answer</summary>

**Correct: C**

FastAPI/Pydantic validation failures default to HTTP 422 Unprocessable Entity automatically, without any custom handler.

**Why the others are wrong:**
- 400 is a generic client error most commonly raised manually via HTTPException, not FastAPI's automatic validation default.
- 500 indicates a server-side failure, not a client validation problem.
- 409 indicates a resource conflict, unrelated to missing fields.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A FastAPI route returns a database ORM object containing a hashed_password field. Which configuration ensures the password is never exposed in the API response?

A) Define a response_model Pydantic schema excluding the password field
B) Set status_code=204 on the route
C) Add a global exception handler for the field
D) Use Depends() to strip the field at request time

<details>
<summary>Answer</summary>

**Correct: A**

response_model filters and serializes the outgoing data against a defined schema, so any field not included (like hashed_password) is automatically excluded from the response.

**Why the others are wrong:**
- 204 means no content at all — it is not a field-filtering mechanism and breaks normal response bodies.
- Exception handlers respond to errors, not shape successful response bodies.
- Depends() injects data/logic into the request handling, not the outgoing response serialization.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which HTTP method is defined as idempotent, meaning repeated identical requests result in the same server state as a single request?

A) POST
B) PATCH
C) CONNECT
D) PUT

<details>
<summary>Answer</summary>

**Correct: D**

PUT replaces the entire resource with the given representation; repeating the same PUT produces the same end state, making it idempotent.

**Why the others are wrong:**
- POST typically creates a new resource on each call, producing different results (e.g., duplicate records) — not idempotent.
- PATCH applies partial modifications and is not guaranteed idempotent depending on the operation semantics used.
- CONNECT is used for tunneling connections, not resource state semantics, and isn't tested for idempotency.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

