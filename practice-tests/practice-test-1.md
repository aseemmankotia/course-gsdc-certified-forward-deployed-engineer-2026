# Practice Test 1: GSDC CFDE Certification: Forward Deployed Engineer Prep

- **Questions:** 45
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** A Forward Deployed Engineer (FDE) is embedded on-site with a logistics client. The VP of Operations says, "Our dispatch process is chaotic and costing us money — fix it with AI." There is no defined dataset, no clear metric, and three different teams describe the problem differently. What should the FDE do FIRST?

A) Ask the client's data team to export all dispatch logs so a predictive model can be trained immediately
B) Recommend the client purchase a commercial dispatch-optimization SaaS product to avoid building anything custom
C) Build a quick proof-of-concept model using whatever data is available so the client can see visible progress within the first week
D) Decompose the stated problem into its component sub-processes and interview each of the three teams to identify where their descriptions converge and diverge before proposing any technical solution

---

**Q2.** Which statement most accurately distinguishes the Forward Deployed Engineer (FDE) role from a traditional Solutions Architect role, per the GSDC CFDE framing?

A) An FDE only writes documentation and design diagrams, while a Solutions Architect writes and ships production code
B) An FDE exclusively works on internal company infrastructure, while a Solutions Architect only works with external clients
C) An FDE and a Solutions Architect perform an identical function, differing only in job title used by the employer
D) An FDE is embedded directly with the client, iterating hands-on through both business translation and implementation of the solution, whereas a Solutions Architect typically designs the technical architecture and hands off implementation to other delivery teams

---

**Q3.** An FDE is decomposing a client's vague request to 'reduce customer churn' using a first-principles approach. Which action best reflects first-principles thinking as opposed to pattern-matching from a prior project?

A) Breaking 'churn' down into its fundamental drivers specific to this client (e.g., pricing complaints, support response time, product usage drop-off) before deciding on any modeling approach
B) Reusing the churn-prediction pipeline from a previous unrelated client because it worked well there
C) Asking the client which vendor tool their competitors use for churn reduction and replicating that choice
D) Assuming churn is caused by pricing because that is the most common cause cited in industry case studies

---

**Q4.** During an initial client discovery session, a stakeholder gives the FDE a large amount of information, including business goals, unrelated organizational politics, technical constraints, and several personal opinions about competitor products. Applying the FDE principle of separating signal from noise, which pieces of information should the FDE prioritize as 'signal' for structuring the problem?

A) The stakeholder's personal opinions about which competitor product is best
B) Organizational politics and interpersonal dynamics mentioned during the meeting
C) All information should be weighted and treated as equally important input
D) Concrete business goals, explicit technical constraints, and measurable success criteria relevant to the problem being solved

---

**Q5.** An FDE is scoping a new engagement and applies an input-processing-output mental model to a client's request to 'automate invoice reconciliation.' The client has already specified the input documents (invoices and purchase orders in PDF) and the desired output (a matched/unmatched report), but has not defined the processing step. Which action correctly applies the input-processing-output model to move the engagement forward?

A) Define the transformation logic needed to go from raw PDF inputs to the matched/unmatched report — including extraction, field mapping, and matching rules — before selecting any specific tool or vendor
B) Skip directly to selecting a specific OCR vendor since the input format (PDF) is already known
C) Ask the client to also redefine the output format since the processing step is unclear
D) Assume the output report is wrong and ask the client to restart requirements gathering from scratch

---

**Q6.** A team is building a FastAPI microservice where every route handler needs a validated database session that must be properly closed after the response is sent, and the team also needs to be able to swap in a mock session during unit tests. Which approach BEST meets these requirements?

A) Open a new database connection manually at the start of every route handler function and close it explicitly at the end of the handler body
B) Define a dependency function that uses `yield` to provide a database session, wrapped with FastAPI's `Depends()`, so the session is closed after the response is sent and can be overridden in tests
C) Open a single global database connection at application startup and reuse it across all requests without per-request scoping
D) Use middleware to attach a new database connection to `request.state` for each incoming request, without adding any explicit connection-closing logic

---

**Q7.** In production, Service A makes a synchronous REST call to Service B on every incoming request. When Service B experiences high latency, Service A's worker threads block waiting on the response, and the entire system becomes unresponsive. Which change BEST improves the resilience of this inter-service communication?

A) Wrap the call to Service B in a circuit breaker that enforces a request timeout and returns a fallback response when Service B is unhealthy or slow
B) Increase the HTTP client timeout in Service A's calls to Service B so requests have more time to complete
C) Migrate Service B to a faster database engine to reduce its response times
D) Deploy additional instances of Service A behind a load balancer to handle more concurrent blocked requests

---

**Q8.** A team needs reproducible builds for a Python microservice: a lock file that pins the exact resolved versions of all transitive dependencies across every environment, plus built-in tooling to build and publish the package. Which dependency management tool BEST fits this requirement?

A) pip together with a manually maintained `requirements.txt` file listing only top-level dependencies
B) conda environments, which are primarily designed around scientific/data-science package channels rather than a build-and-publish workflow for Python packages
C) poetry, which resolves dependencies, generates a `poetry.lock` file pinning exact transitive dependency versions, and provides built-in commands for building and publishing packages
D) A plain virtualenv with no dependency-manifest or lock file

---

**Q9.** A FastAPI endpoint declares a request body using a Pydantic model. When a client sends a JSON payload that fails validation against that model (for example, a required field is missing), what HTTP status code does FastAPI automatically return?

A) 400 Bad Request
B) 422 Unprocessable Entity
C) 500 Internal Server Error
D) 404 Not Found

---

**Q10.** Which statement correctly differentiates the HTTP PUT and PATCH methods in a REST API contract?

A) PUT is used exclusively to create new resources, while PATCH is used exclusively to update existing ones
B) PATCH is idempotent by definition while PUT is not guaranteed to be idempotent
C) PUT and PATCH are interchangeable in REST API design and differ only by naming convention
D) PUT is idempotent and expects the request body to replace the entire target resource, while PATCH applies a partial modification to the resource

---

**Q11.** An internal service-to-service API needs a lightweight authentication mechanism where each calling service presents a static credential to identify itself. There's no end user involved, no need to track sessions, and keys are rotated manually on a schedule. Which authentication mechanism BEST fits this requirement?

A) OAuth2 authorization code flow, requiring a browser-based user consent screen for each service
B) JWT access tokens issued with short expirations plus a refresh-token flow to renew them
C) Server-side session cookies backed by a centralized session store
D) A static API key sent in a request header and validated against a set of stored, manually-rotated keys

---

**Q12.** An FDE is building a FastAPI endpoint that handles POST /clients to create a new client record in the database. The record is successfully created and its data is returned in the response body. Which HTTP status code should the endpoint return?

A) 200 OK
B) 201 Created
C) 202 Accepted
D) 204 No Content

---

**Q13.** A project's pyproject.toml declares a dependency as requests = "^2.31.0" using Poetry's caret versioning syntax. Which range of installed versions does this constraint allow?

A) Exactly version 2.31.0 and no other version
B) Any version >=2.31.0 and <3.0.0
C) Any version >=2.31.0, including 3.0.0 and above, with no upper limit
D) Any version >=2.31.0 and <2.32.0

---

**Q14.** A retail company ingests raw clickstream data into a cloud data warehouse with virtually unlimited elastic compute and storage (e.g., Snowflake). They want to preserve the raw, unaltered data for future reprocessing needs and let analysts transform it using SQL directly inside the warehouse. Which approach BEST fits this requirement?

A) ELT — load the raw data into the warehouse first, then transform it using the warehouse's native SQL compute
B) ETL — transform the data on a separate on-premises server before loading it into the warehouse
C) ELT — stage the raw data in a NoSQL document store and transform it there before loading to the warehouse
D) ETL — stream pre-transformed events directly into a dashboard, bypassing the warehouse

---

**Q15.** A bank must detect fraudulent transactions and block them within 200 milliseconds of occurrence, before the transaction settles. Which pipeline pattern should the FDE recommend?

A) A nightly batch job using Spark to aggregate the day's transactions
B) A micro-batch job that runs every 15 minutes
C) A streaming pipeline using a message broker (e.g., Kafka) with real-time stream processing
D) A manual daily export/import process using CSV files

---

**Q16.** An FDE is building a RAG system that must retrieve the top-k most semantically similar document chunks to a user's query embedding in near real-time, at a scale of 50 million vectors. Which storage solution is BEST suited for this requirement?

A) A purpose-built vector database (e.g., Pinecone, Weaviate) using approximate nearest neighbor (ANN) indexing
B) A document-oriented NoSQL store like MongoDB using exact key lookups
C) A relational SQL database using a B-tree index on the embedding column
D) An in-memory key-value store using hash-based lookups

---

**Q17.** A model predicts whether a rare manufacturing defect will occur; only 2% of parts are defective. The business wants to minimize the number of defective parts that slip through undetected, even if that means flagging some good parts unnecessarily. Which metric should the FDE prioritize when tuning the model?

A) Accuracy
B) Specificity for the non-defective class
C) Recall (sensitivity) for the defective class
D) R-squared

---

**Q18.** An FDE has a dataset of 500 labeled examples for a binary classification task with a 90/10 class imbalance. To get a reliable performance estimate while ensuring each fold maintains the original class ratio, which cross-validation configuration should be used?

A) Simple k-fold cross-validation with k=2
B) Leave-one-out cross-validation
C) Stratified k-fold cross-validation with k=5 or k=10
D) A single 50/50 train-test split

---

**Q19.** In transformer architecture, what is the primary purpose of the self-attention mechanism?

A) To reduce the dimensionality of input embeddings before classification
B) To allow each token in a sequence to weigh the relevance of every other token when computing its own representation
C) To convert text tokens into byte-pair encoded subwords
D) To normalize gradients during backpropagation to prevent vanishing gradients

---

**Q20.** An FDE is deploying a customer support system that needs to retrieve semantically similar past tickets based on meaning, not exact keyword matches, from a corpus of 2 million historical tickets. Which storage solution BEST meets this requirement?

A) A relational SQL database with full-text search indexes on the ticket body column
B) A vector database storing embeddings generated from the ticket text, queried via approximate nearest neighbor search
C) A NoSQL document store with tickets indexed by customer ID and timestamp
D) An in-memory key-value cache storing the most recently accessed tickets

---

**Q21.** A model built to predict fraudulent transactions is evaluated on a test set where only 2% of transactions are fraudulent. The model achieves 98% accuracy but flags almost no actual fraud cases. Which metric should the FDE prioritize instead of accuracy to properly evaluate this model?

A) R-squared
B) Mean Absolute Error
C) Recall (sensitivity) on the fraud class
D) Silhouette score

---

**Q22.** In a transformer architecture, what is the primary function of the self-attention mechanism?

A) It reduces the dimensionality of input embeddings before they enter the feed-forward layers
B) It converts raw text tokens into their corresponding numerical vector embeddings
C) It allows each token in a sequence to weigh the relevance of every other token when computing its contextual representation
D) It compresses the entire input sequence into a single fixed-length vector before decoding

---

**Q23.** A team builds a RAG system over 500-page legal contracts. Users ask about a payment-terms clause but the system returns text about an unrelated warranty section. The pipeline uses fixed 512-token chunks with zero overlap and retrieves the top-3 chunks by cosine similarity. Which change is MOST likely to fix this?

A) Increase chunk size to 4000 tokens so more context is captured per chunk
B) Switch to semantic or structure-aware chunking with overlap so individual clauses stay intact within a chunk
C) Increase top-k retrieval to 20 chunks so the correct one is more likely included
D) Replace the generation LLM with a larger, more capable model

---

**Q24.** A team is moving a RAG prototype into production. Production requirements are: horizontal scalability to tens of millions of vectors, built-in metadata filtering on queries, multi-region replication, and no infrastructure operated by the team itself. Which option BEST satisfies these requirements?

A) FAISS, used as an in-process library within the application server
B) Chroma running as an embedded local instance on a single machine
C) Pinecone, a fully managed vector database service
D) A relational database with a manually written cosine-similarity SQL function

---

**Q25.** An FDE builds a pipeline using an LLM's JSON mode / structured output feature and needs the downstream parser to never crash in production. Despite JSON mode being enabled, which practice is still mandatory?

A) Set temperature to 1.0 to maximize output diversity
B) Skip schema validation entirely since JSON mode guarantees a schema-conformant response
C) Programmatically parse and validate every response against the expected schema, with a retry or fallback path on failure
D) Set max_tokens to unlimited so the JSON is never truncated

---

**Q26.** Which statement correctly distinguishes chain-of-thought (CoT) prompting from few-shot prompting?

A) CoT provides multiple labeled input-output example pairs; few-shot asks the model to show step-by-step reasoning before its final answer
B) CoT and few-shot are the same technique and differ only in the temperature setting used
C) Few-shot only functions with base (non-instruction-tuned) models, while CoT only functions with instruction-tuned models
D) Few-shot provides multiple examples of the task to imitate; CoT prompts the model to produce intermediate reasoning steps before its final answer

---

**Q27.** A RAG chatbot for product support frequently gives confident, factually wrong answers when the retrieved chunks do not actually contain the relevant information -- the LLM fills the gap using its own parametric knowledge instead of flagging insufficient context. Which mitigation directly addresses this failure mode?

A) Instruct the model explicitly in the system prompt to respond 'insufficient context' when the retrieved chunks don't contain the answer, and add a groundedness/relevance check on retrieved chunks before generation
B) Increase the embedding model's output dimensionality
C) Reduce the number of retrieved chunks passed to the generator to exactly one
D) Switch to a model with a larger context window

---

**Q28.** An FDE needs an agent that alternates between reasoning about what to do next and invoking external tools (search, calculator) based on that reasoning, continuing this loop until it has enough information to answer. Which pattern is specifically designed for this interleaved reasoning-and-acting behavior?

A) ReAct (Reasoning + Acting)
B) Self-consistency prompting
C) Zero-shot prompting
D) Fixed-order prompt chaining with no branching

---

**Q29.** A team built a RAG system over technical documentation containing mixed code snippets and prose. They use fixed 512-token chunks with zero overlap, split purely by token count. Users now report that answers reference broken, incomplete code where functions are cut off mid-body. Which fix BEST addresses the root cause?

A) Use structure-aware chunking that splits on document boundaries like code fences and headers, with small overlap between chunks
B) Increase the fixed chunk size to 2048 tokens across the entire corpus
C) Switch to a higher-dimensional embedding model to capture more context per chunk
D) Add a re-ranking step after retrieval to reorder the returned chunks

---

**Q30.** A RAG system uses pure dense vector search over document embeddings. Users searching for an exact product code, e.g. "SKU-48291", get irrelevant results even though that exact string appears verbatim in the corpus. Which change BEST resolves this failure mode?

A) Increase top-k so more candidate chunks are retrieved and passed to the LLM
B) Fine-tune the LLM generator on more question-answer pairs from the domain
C) Implement hybrid retrieval that combines dense vector search with sparse keyword search such as BM25
D) Switch to an LLM with a larger context window so more chunks fit in the prompt

---

**Q31.** A team wants to evaluate RAG answer quality at scale using an LLM-as-judge pattern instead of relying solely on human reviewers. What is the primary risk they must account for with this approach?

A) LLM-as-judge evaluation cannot be automated or run in a pipeline
B) LLM-as-judge only produces categorical scores and cannot output numeric ratings
C) The judge model may share biases or blind spots with the model being evaluated, causing it to systematically overrate certain error types
D) LLM-as-judge requires the evaluated system to output strict JSON, making it incompatible with free-text answers

---

**Q32.** A client needs an automated system to process incoming invoices: extract vendor name, amount, and date, validate against a fixed set of business rules, and route to one of three approval queues. The steps never change and must run in under 200ms with 100% predictable behavior. Which approach BEST fits this requirement?

A) Use a deterministic pipeline with direct function calls for extraction, validation, and routing — no agent reasoning loop
B) Build a multi-agent system with a planner agent and an executor agent for flexibility
C) Use a ReAct-style agent with tool calling and automatic retries
D) Use a LangChain agent configured with long-term memory to learn invoice patterns over time

---

**Q33.** In a multi-agent system, a 'researcher' agent and a 'critic' agent keep passing the same task back and forth, each rejecting the other's output without converging, and the process never terminates. What is the BEST first fix?

A) Add a third agent to break the tie between the researcher and critic
B) Increase the temperature setting so the agents generate more varied responses
C) Give both agents access to additional external tools
D) Introduce a maximum iteration limit and a supervisor agent with an explicit termination condition

---

**Q34.** An FDE needs to build two client deliverables during a two-week sprint: (1) a multi-page internal analytics dashboard with custom layouts, session state, and interactive widgets for the client's ops team, and (2) a fast demo interface showing an image classification model's predictions for a live client presentation. Which tool pairing is BEST?

A) Use Gradio for both the dashboard and the model demo
B) Use Streamlit for both the dashboard and the model demo
C) Use Gradio for the dashboard and Streamlit for the model demo
D) Use Streamlit for the dashboard and Gradio for the ML model demo

---

**Q35.** To optimize Docker build times for a Python AI application by taking advantage of layer caching, which Dockerfile instruction order is BEST?

A) COPY the entire application directory first, then run pip install on requirements.txt
B) COPY requirements.txt first, run pip install, then COPY the rest of the application code
C) Combine the dependency install and code copy into a single RUN command at the end of the file
D) COPY the application code and requirements.txt together in one step, then run pip install

---

**Q36.** An FDE discovers that a client's OpenAI API key was hardcoded directly into a Dockerfile that was committed and pushed to a public GitHub repository. What is the CORRECT immediate remediation?

A) Immediately rotate/revoke the exposed key, move secrets to environment variables or a secrets manager, and scrub the key from git history
B) Add the Dockerfile to .gitignore so it isn't tracked going forward
C) Wait to change the key until unauthorized usage is actually detected on the billing dashboard
D) Encrypt the Dockerfile with a password before the next commit

---

**Q37.** In agentic system design, which memory type refers to information retained only within the scope of a single conversation or session and discarded once that session ends?

A) Long-term memory
B) Episodic memory
C) Short-term memory
D) Vector memory

---

**Q38.** A forward deployed engineer is finalizing a Dockerized FastAPI service that calls a third-party LLM API. The client's security team requires that no API key ever appear inside the built image or the Git history. Which approach BEST satisfies this requirement?

A) Inject the API key as an environment variable at container runtime, sourced from a secrets manager (e.g., AWS Secrets Manager, Azure Key Vault, or a Kubernetes Secret)
B) Add the API key as an ENV instruction in the Dockerfile so it is available to the container at runtime
C) Store the API key in a .env file, COPY it into the image during the build, and load it with a library like python-dotenv
D) Store the API key directly in the application source code and restrict repo access to a private GitHub repository

---

**Q39.** A client needs an application that reads scanned invoices, extracts vendor name, invoice number, and total amount into fixed fields, and writes them to a Postgres table. The steps never change and must run reliably at high volume. Which design is the BEST fit?

A) A multi-agent system with a planner agent that delegates sub-tasks to a retriever agent and a database agent
B) A ReAct-style agent loop that reasons step-by-step and decides at each turn which tool to call next until the task is complete
C) A single agent equipped with long-term episodic memory so it can recall how previous invoices were formatted
D) A single LLM call using function/tool calling to extract the three structured fields, followed by a deterministic script that validates and inserts the data into Postgres

---

**Q40.** A mid-size retailer's VP of Operations requests a live demo of an AI inventory forecasting tool for the executive team next week. During prep, the FDE discovers the model's accuracy has degraded due to recent data drift. What is the BEST next step?

A) Proceed with the demo using cached historical outputs so the issue isn't visible to executives
B) Cancel the entire engagement, citing unacceptable technical risk
C) Postpone indefinitely without giving the client a reason, until the model is fully retrained
D) Inform the stakeholder transparently, propose a demo with clearly caveated or delayed-refresh data, and present a concrete mitigation timeline

---

**Q41.** During a live demo, an executive asks a pointed question about data privacy compliance that the FDE cannot fully answer on the spot. What is the BEST response?

A) Improvise a plausible-sounding answer to keep the meeting's momentum and confidence high
B) Acknowledge the gap honestly, commit to a specific follow-up date with a documented action item, and continue the demo
C) Tell the executive the question isn't relevant to today's demo and move on
D) Deflect by redirecting the conversation to a different, more favorable topic

---

**Q42.** During discovery, an FDE needs to identify which stakeholders hold the most influence and interest in a proposed AI initiative, in order to prioritize workshop invitees. Which technique BEST supports this specific goal?

A) A RACI matrix limited to project task assignments
B) A power-interest grid mapping each stakeholder's influence level against their level of interest
C) A SWOT analysis of the client's overall organization
D) A static org chart review of formal reporting lines

---

**Q43.** When structuring a demo using the problem-insight-solution-impact narrative arc, which sequencing produces maximum impact for an executive audience?

A) Solution, Problem, Insight, Impact
B) Problem, Insight, Solution, Impact
C) Problem, Solution, Insight, Impact
D) Insight, Problem, Impact, Solution

---

**Q44.** What primarily differentiates a trusted-advisor engagement model from a standard vendor engagement in long-term FDE client relationships?

A) The trusted-advisor model centers on proactive, unbiased guidance tied to the client's business outcomes rather than product upsell
B) The trusted-advisor model exclusively requires on-site presence with no remote engagement allowed
C) The trusted-advisor model removes the need to track success metrics since the relationship is based on trust alone
D) The trusted-advisor model is defined mainly by shorter contract renewal cycles

---

**Q45.** A client's CFO questions the ROI justification for a proposed RAG-based support automation MVP costing $250K, with projected annual savings of $400K from reduced support headcount. Which approach BEST strengthens the business case for CFO approval?

A) Emphasize the technical sophistication of the RAG architecture and model accuracy benchmarks
B) Guarantee the $400K savings figure as a contractually binding outcome to build confidence
C) Skip financial specifics and instead emphasize competitive pressure from other companies adopting AI
D) Present the payback period, a sensitivity analysis on the savings assumptions, and a phased investment plan tied to milestone-based validation

---

