# Practice Test 2: GSDC CFDE Certification: Forward Deployed Engineer Prep

- **Questions:** 45
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A retail client tells an FDE: 'Our inventory forecasting is broken — just give us an AI model that fixes it.' The client's data team, ops team, and finance team each describe different symptoms with no shared definition of 'broken.' Following FDE problem-structuring practice, what should the FDE do BEFORE proposing any technical solution?

A) Build a quick forecasting model using historical sales data to demonstrate value fast, then refine based on team feedback
B) Facilitate a structured session to decompose 'broken' into mutually exclusive, collectively exhaustive failure categories (e.g., data quality, model accuracy, process latency, stakeholder misalignment) and map each to a distinct root cause before scoping any technical work
C) Ask the client's IT department to provide full system documentation and API specs so the FDE can assess technical feasibility first
D) Recommend the client purchase an off-the-shelf forecasting platform since three departments disagreeing signals a process problem, not a technical one

---

**Q2.** Which statement BEST captures the core distinction between a Forward Deployed Engineer (FDE) and a Solutions Architect when both are engaged on the same enterprise AI deployment?

A) The FDE focuses solely on writing production code while the Solutions Architect handles all client communication
B) The Solutions Architect designs the reference architecture and hands it off, while the FDE embeds with the client, iterates the solution against live production constraints, and owns delivery outcomes end-to-end
C) There is no meaningful distinction; both roles are interchangeable titles for the same on-site technical consulting function
D) The FDE only works on internal company tools, whereas the Solutions Architect is the only role that engages directly with external clients

---

**Q3.** During discovery, a logistics client insists the new system must provide 'real-time' shipment predictions, but the FDE learns that the client's warehouse scanners only sync inventory data to the central database once every 6 hours via batch upload. Applying constraint and feasibility analysis, what should the FDE do?

A) Proceed with building a real-time streaming pipeline as requested, since data latency can be optimized later in a future phase
B) Recommend the client replace all warehouse scanners with IoT-enabled real-time sensors as a prerequisite to any project kickoff
C) Silently design the system assuming 6-hour batches and let the client discover the actual latency during UAT
D) Surface the data-freshness constraint immediately, reframe 'real-time' with the client into an achievable definition (e.g., 'near-real-time within the 6-hour sync window') and negotiate scope before any architecture is chosen

---

**Q4.** An FDE is conducting stakeholder interviews for a new client engagement and receives contradictory requirements from five different business units. Which technique is MOST appropriate for the FDE to apply to separate signal from noise in these requirements?

A) A MECE-structured requirements matrix that categorizes each stated need into non-overlapping, exhaustive buckets, then cross-references frequency and business impact to identify true priority signals
B) SWOT analysis to catalog strengths and weaknesses of each business unit's current process
C) A simple majority vote among stakeholders to determine which requirements to implement first
D) First-principles re-derivation of the client's entire business model from scratch before considering any stated requirement

---

**Q5.** A hospital administrator tells an FDE: 'We want AI to reduce patient wait times.' Using the input-processing-output mental model to translate this business ask into a technical problem statement, what is the FDE's correct FIRST step?

A) Identify and validate the actual data inputs available (e.g., check-in timestamps, staff schedules, historical throughput) and the specific output metric the administrator means by 'reduced wait times' before deciding on any processing approach
B) Immediately propose a triage-prediction ML model, since reducing wait times is a well-known use case in healthcare AI
C) Ask the administrator to define the required cloud infrastructure budget so the FDE can size compute for the output model
D) Deploy a pilot dashboard showing current wait times to buy time while the FDE studies the codebase

---

**Q6.** A team built a FastAPI service where all route handlers are declared with `async def`. One handler calls a synchronous third-party SDK function that performs a blocking network call taking 3 seconds. Under load testing with 50 concurrent requests, overall response times degrade far more than the 3-second SDK latency alone would explain. What is the BEST fix?

A) Increase the number of Uvicorn worker processes handling the application
B) Wrap the blocking call in `asyncio.sleep()` to yield control back to the event loop
C) Add stricter Pydantic response validation to reduce serialization overhead
D) Change the route handler from `async def` to `def`, allowing FastAPI to execute it in its internal thread pool

---

**Q7.** A project's `poetry.lock` file pins `fastapi==0.104.1`, but a teammate's local environment reports `fastapi==0.109.0` after they ran `pip install fastapi --upgrade` directly. Which command restores their environment to match the versions the team has locked and tested?

A) Run `poetry install` to install the exact versions pinned in poetry.lock
B) Run `poetry update fastapi` to align the environment with the latest release
C) Run `poetry add fastapi@latest` to force reinstall the package
D) Run `pip freeze > requirements.txt` and reinstall from that file

---

**Q8.** An enterprise client requires that a public-facing API issue short-lived, stateless credentials that embed user role claims and can be independently verified by multiple downstream microservices without querying a shared session store. Which authentication approach BEST meets this requirement?

A) Database-backed API keys validated by each microservice against a shared table
B) JWTs signed with a shared secret or public key, containing role claims and a short expiration
C) HTTP Basic Authentication with per-request password hashing
D) Server-side session cookies backed by a centralized session store

---

**Q9.** You need a Pydantic v2 model field `age` that must be an integer, is required, and accepts any value from 0 through 120 inclusive, rejecting negative numbers and values above 120. Which field definition is correct?

A) age: int = Field(..., ge=0, le=120)
B) age: int = Field(..., min=0, max=120)
C) age: int = Field(..., gt=0, lt=120)
D) age: conlist(int, min_items=0, max_items=120)

---

**Q10.** In a production Python service with a retry mechanism, an operation fails on its first attempt but is automatically retried and no operator action is required at this point. Which logging level is MOST appropriate for this specific log entry?

A) DEBUG
B) CRITICAL
C) ERROR
D) WARNING

---

**Q11.** Service A must notify Service B whenever an order is placed. Service B's processing can take up to 30 seconds, and Service A must not block or wait for that processing to complete before responding to its own caller. Which inter-service communication pattern is BEST?

A) Make a synchronous REST call from Service A to Service B with a 30-second timeout
B) Use a gRPC unary call with automatic client-side retries
C) Publish an event to a message queue (e.g., Kafka or RabbitMQ) for Service B to consume asynchronously
D) Have Service A write directly to Service B's database table

---

**Q12.** A Forward Deployed Engineer builds a FastAPI service where each request must acquire a database connection from a pool, use it to execute a query, and always release it back to the pool — even if the route handler raises an unhandled exception. Which dependency function implementation correctly guarantees the connection is released in every case?

A) def get_db():
    conn = pool.acquire()
    return conn
B) def get_db():
    conn = pool.acquire()
    yield conn
    pool.release(conn)
C) def get_db():
    conn = pool.acquire()
    try:
        yield conn
    finally:
        pool.release(conn)
D) async def get_db():
    conn = await pool.acquire()
    yield conn

---

**Q13.** Service A must notify Services B, C, and D whenever a new order is created. The order-creation request must not fail or block if Service C is temporarily down, and new consumer services should be addable later without modifying Service A's code. Which inter-service communication pattern BEST meets these requirements?

A) Service A makes sequential synchronous HTTP POST calls to B, C, and D inside a try/except block, logging any failures
B) Service A publishes an 'OrderCreated' event to a message broker (e.g., Kafka or RabbitMQ), and B, C, and D each subscribe independently
C) Service A calls an API gateway that fans out synchronous calls to B, C, and D concurrently using asyncio.gather with return_exceptions=True
D) Service A writes the new order directly into a shared database table that B, C, and D each poll on a schedule

---

**Q14.** A fintech company processes credit card transactions and must flag potential fraud within 200ms of each transaction occurring, using continuously updated behavioral features. Which data pipeline pattern BEST meets this requirement?

A) A streaming pipeline (e.g., Kafka + stream processor) that computes and scores features in real time as events arrive
B) Nightly batch ETL job that recomputes fraud scores for all transactions from the previous day
C) Micro-batch processing every 15 minutes using scheduled Spark jobs
D) An ELT pipeline that loads raw transactions into a data warehouse for the fraud analytics team to query on demand

---

**Q15.** A team building a RAG chatbot needs to store 2 million document chunks and retrieve the most semantically similar chunks to a user's query in milliseconds. Which storage solution is the BEST fit?

A) Relational SQL database with full-text search indexes
B) Key-value NoSQL store like Redis for caching
C) Vector database using approximate nearest neighbor (ANN) search
D) In-memory JSON store with linear string matching

---

**Q16.** You are tuning a binary classifier for a highly imbalanced dataset (2% positive class) using k-fold cross-validation. Which configuration choice is MOST important to avoid biased performance estimates?

A) Increase k to 20 folds instead of 5 to get more granular estimates
B) Use leave-one-out cross-validation to maximize training data per fold
C) Use a single 80/20 train-test split instead of k-fold cross-validation
D) Use stratified k-fold so each fold preserves the original class ratio

---

**Q17.** What is the primary advantage of the self-attention mechanism in transformer architectures compared to the sequential processing in RNNs?

A) It allows the model to compute relationships between all tokens in a sequence in parallel, capturing long-range dependencies more efficiently
B) It eliminates the need for positional information about word order
C) It reduces model size by removing the need for embeddings
D) It guarantees lower training loss than any RNN-based architecture

---

**Q18.** A data scientist trained a model last quarter that performed well, but the team can no longer reproduce those exact results despite having the saved model file. Which combination of logged artifacts would have MOST reliably ensured reproducibility?

A) Model accuracy score and confusion matrix screenshot
B) The final trained model weights only
C) A written summary of the modeling approach in a shared document
D) Code commit hash, exact dataset version/hash, hyperparameters, and library/environment versions

---

**Q19.** A company wants to automatically route incoming support tickets into exactly 5 fixed categories based on well-defined keyword rules (e.g., the word 'refund' in a ticket always maps to 'Billing'), and these rules rarely change. Which approach is MOST appropriate?

A) Deploy a rule-based system using keyword/pattern matching
B) Fine-tune a large language model for ticket classification
C) Train a deep learning transformer classifier from scratch
D) Use a vector database with semantic similarity search to find the closest category

---

**Q20.** A fraud-detection team needs to score incoming payment transactions in near real time and be automatically alerted when the incoming feature distributions start drifting from training data. Which architecture BEST meets these requirements?

A) A nightly batch ETL job that recomputes fraud rules and emails flagged transactions to the compliance team
B) An ELT pipeline loading transactions into a cloud data warehouse for daily BI dashboard review
C) A streaming pipeline (e.g., Kafka + online feature store) with low-latency model serving and automated data drift/quality monitoring
D) Storing all transactions in a NoSQL document store and relying on manual analyst review each morning

---

**Q21.** A bank wants to flag potentially fraudulent transactions using 40 numeric features (amount, velocity, geolocation deltas) collected over several years, with millions of labeled historical examples. Regulators require that each flagged decision be explainable, and the system must return a score within a 5ms latency budget per transaction. Which approach BEST satisfies these requirements?

A) Fine-tune a large language model and prompt it with the transaction's feature values written out as natural language text
B) Train a gradient-boosted tree ensemble (e.g., XGBoost) on the labeled data and generate SHAP values for per-decision explainability
C) Have domain experts hand-write threshold-based if-else rules for flagging transactions
D) Build a retrieval-augmented generation system that retrieves similar historical fraud cases from a document store before generating a decision

---

**Q22.** In a standard transformer's self-attention mechanism, computing pairwise attention scores across a sequence of length n costs O(n^2). Which technique is commonly used to reduce this quadratic cost for processing long documents?

A) Increasing the embedding dimension of each token
B) Removing positional encodings from the input sequence
C) Replacing token embeddings with one-hot encoded vectors
D) Using sparse or local attention patterns (e.g., sliding-window attention) so each token attends only to a limited context window

---

**Q23.** A team needs a chain-of-thought math reasoning system to reduce output variance for numeric answers where the LLM is right about 70% of the time on a single attempt. The latency/cost budget allows up to 5x the base call cost. Which technique BEST fits this constraint?

A) Run self-consistency: sample N=5 independent chain-of-thought reasoning paths and take a majority vote on the final answer
B) Increase temperature to 1.0 to encourage more diverse reasoning paths
C) Switch to zero-shot prompting to simplify the reasoning chain
D) Use a single ReAct loop that calls an external calculator tool once

---

**Q24.** A RAG system retrieves the top-10 chunks (about 500 tokens each) and concatenates them into a 16K-token context window, with the highest-scoring chunk placed first and the lowest last. Users report that answers frequently miss facts clearly present in the chunk ranked 5th or 6th. Which of the following best explains this failure mode?

A) The embedding model returned irrelevant chunks, so this is a retrieval failure
B) The LLM's true context limit is lower than 16K tokens, silently truncating the input
C) "Lost in the middle" degradation — LLMs attend less reliably to information positioned in the middle of a long context than to information near the beginning or end
D) The vector database returned duplicate chunks, reducing effective coverage of the context

---

**Q25.** A legal document search RAG system must retrieve results based on both exact citation matches (e.g., 'Section 12.3(a)') and semantic similarity to natural-language queries. Pure dense (embedding-based) retrieval alone performs poorly on citation lookups. Which retrieval architecture BEST addresses this requirement?

A) Increase the embedding dimensionality to improve semantic matching precision
B) Hybrid retrieval combining sparse lexical search (e.g., BM25) with dense vector search, merging results via score fusion such as reciprocal rank fusion
C) Replace the vector database with a relational database using only LIKE-based keyword queries
D) Increase chunk overlap to 50% so citation tokens appear redundantly across more chunks

---

**Q26.** A RAG pipeline retrieves the top-50 candidate chunks from a vector database (optimizing for recall), and must then select a small, highly relevant subset to fit a tight LLM context budget. Which architecture correctly applies a cross-encoder re-ranker in this pipeline?

A) Run the cross-encoder re-ranker on all 50 candidates first, then use its scores to rebuild the vector index for future queries
B) Skip re-ranking entirely since vector similarity scores are already precise enough for final chunk selection
C) Use the cross-encoder to re-score only the single top-ranked vector search result before passing it forward
D) Apply the cross-encoder re-ranker to score each of the 50 candidates against the query, then select the top-N (e.g., top-5) highest-scoring chunks to pass into the LLM prompt

---

**Q27.** A team builds an automated evaluation pipeline using an LLM-as-judge to score 10,000 chatbot responses for helpfulness, calibrated against 200 human-labeled examples. The judge model shows a systematic bias toward favoring longer responses regardless of actual quality. Which mitigation is MOST appropriate?

A) Set the judge model's temperature to 0 to make scoring more consistent
B) Discard the human-labeled examples since the judge's scoring should be independent of human bias
C) Provide the judge with a detailed rubric explicitly instructing it to evaluate helpfulness independent of length, and include length-matched contrastive examples in the judge prompt
D) Replace the LLM-as-judge approach entirely with exact string matching against reference answers

---

**Q28.** Which statement correctly distinguishes the ReAct prompting pattern from the Reflection pattern?

A) ReAct and Reflection are functionally identical, differing only in naming convention across papers
B) ReAct interleaves reasoning traces with actions (e.g., tool calls) and observes results before continuing; Reflection has the model critique and revise its own prior output after generating an initial attempt
C) ReAct is used only within RAG retrieval steps, while Reflection is used only for chain-of-thought math problems
D) Reflection requires access to external tools or an environment, while ReAct does not

---

**Q29.** A retail enterprise's RAG chatbot uses only dense embedding similarity to retrieve top-5 chunks for customer queries. Customers frequently ask about specific SKU numbers and part codes, but the chatbot returns irrelevant chunks because the embedding model treats these alphanumeric codes as semantically similar to unrelated text. Which change BEST fixes this specific failure mode?

A) Increase k to retrieve the top-20 chunks instead of top-5
B) Switch to hybrid retrieval combining BM25 keyword search with dense embeddings, then re-rank the merged results
C) Increase the chunk size so each chunk contains more surrounding context
D) Fine-tune the LLM generator on the enterprise's product catalog

---

**Q30.** An FDE is chunking a 200-page enterprise policy manual for RAG using fixed-size chunking at 512 tokens with no overlap. Evaluation shows the model frequently cites incomplete clauses because policy statements get split across chunk boundaries. Which configuration change BEST addresses this specific failure mode?

A) Reduce chunk size to 256 tokens to make retrieval more granular
B) Increase the number of retrieved chunks (top-k) from 3 to 10
C) Switch to an embedding model with a larger output dimension
D) Add 10-15% token overlap between adjacent chunks and attach section-header metadata to each chunk

---

**Q31.** An FDE builds a workflow for multi-step arithmetic reasoning where the model samples several independent chain-of-thought reasoning paths at higher temperature (no external tool calls) and the final answer is chosen by majority vote across the sampled paths. Which technique does this describe?

A) Self-consistency
B) ReAct
C) Reflection
D) Few-shot chain-of-thought prompting

---

**Q32.** A client asks you to automate their invoice intake process: extract fields from PDF invoices, validate the total against a purchase order in their ERP, and route the invoice to the correct approver based on a fixed amount threshold. The steps never branch based on judgment calls, and no external research or dynamic tool selection is needed. Which approach BEST fits this requirement?

A) Build a ReAct-style agent that autonomously decides which tool to call at each step (OCR, ERP lookup, routing)
B) Deploy a multi-agent system with separate extraction, validation, and routing agents that negotiate the final decision
C) Use a deterministic pipeline: an LLM call for field extraction, followed by rule-based validation and routing logic
D) Use a single agent with long-term memory so it learns invoice formatting patterns over time

---

**Q33.** In a production multi-agent system, a researcher agent and a writer agent are designed to collaborate: the writer requests more research whenever it judges the draft insufficient. In testing, the two agents occasionally loop for over 40 turns without producing a final answer, consuming excessive tokens. Which fix BEST addresses this reliability issue?

A) Increase the context window size so both agents retain more history and avoid redundant requests
B) Raise the temperature setting on both agents' LLM calls to encourage more varied responses
C) Introduce a maximum iteration limit enforced by a supervisor process that escalates to human review if the limit is exceeded
D) Remove the writer agent entirely and have the researcher agent produce the final output directly

---

**Q34.** A customer support agent must recall the resolution of a specific ticket a customer references three weeks later, in a completely new session with no shared conversation history. Which memory architecture is required to support this?

A) Short-term memory: a conversation buffer that holds recent turns within the active session
B) A working memory scratchpad that is cleared after each tool call completes
C) Episodic memory persisted in a vector database, indexed by customer ID and interaction timestamp, retrieved via semantic search at session start
D) Parametric memory encoded directly into the model's weights via periodic fine-tuning

---

**Q35.** Your team is containerizing a Python AI application whose build process requires compiling several packages with native dependencies, but the runtime only needs the compiled artifacts. Which Dockerfile strategy produces the smallest, most secure production image?

A) A single-stage Dockerfile using `python:3.12-slim` as the base, running `pip install` for all build and runtime dependencies together
B) A multi-stage build: a builder stage using the full `python:3.12` image to compile and install dependencies into a virtual environment, then a final stage using `python:3.12-slim` that copies only the virtual environment from the builder
C) Building the image interactively by running a container, installing dependencies manually, then using `docker commit` to save it as the production image
D) Creating a separate Docker image per dependency and combining them at runtime using a Docker manifest list

---

**Q36.** A client's chatbot backend calls an LLM API for every incoming user question. Analytics show thousands of near-duplicate questions phrased differently by different users each day, driving up API costs. Which caching strategy is MOST effective at reducing redundant LLM calls without degrading response relevance?

A) Exact-match caching keyed on the raw, normalized query string
B) Semantic caching that embeds each incoming query and serves a cached response when cosine similarity to a stored query exceeds a defined threshold
C) Time-based caching that stores every response and invalidates all entries after a fixed 24-hour window
D) Disabling caching entirely and relying on the LLM provider's own infrastructure-level response caching

---

**Q37.** You need to build a client-facing prototype with multiple distinct pages (dashboard, chat interface, analytics view), a persistent sidebar for navigation between them, and token-by-token streaming of LLM responses in the chat page. Which approach BEST fits these requirements?

A) A Streamlit multipage app using the `pages/` directory structure with sidebar navigation and `st.write_stream` for token streaming
B) Gradio Blocks with tabs used to simulate separate pages within a single interface
C) Gradio's `ChatInterface` component with custom CSS overrides to add dashboard and analytics sections
D) A single-page Streamlit app using `st.expander` sections to visually separate the dashboard, chat, and analytics content

---

**Q38.** An FDE is building a client-facing support tool that answers questions strictly from a fixed 200-page product manual. Each query requires exactly one retrieval step followed by one generation step—no branching logic, no external tool calls, and no need to remember prior turns since queries are independent. The client wants sub-second responses at high volume (500+ queries/hour) and predictable costs. Which architecture BEST fits these requirements?

A) A multi-agent system with a planner agent that delegates to a retriever agent and a verifier agent for quality control
B) A single-pass RAG pipeline (retrieve-then-generate) with no agentic loop, since the task has no multi-step reasoning, no tool orchestration decisions, and no state to track
C) An agent with function calling that decides at runtime whether to query the manual, call a web search tool, or ask a clarifying question
D) An agent with episodic memory so it can recall similar past questions from other users and adapt its retrieval strategy

---

**Q39.** During a client demo, an FDE's deployed LLM-backed API sees 50 concurrent users repeatedly asking the same top-10 FAQ-style questions, causing costs to spike and response times to degrade because every request triggers a fresh LLM call. The model itself is already appropriately sized for the task. Which change BEST reduces cost and latency without altering the model or degrading the experience for legitimate distinct queries?

A) Scale out by adding more container replicas behind the load balancer to handle the concurrent load
B) Add per-user rate limiting capped at 10 requests per minute to control the volume of calls hitting the model
C) Swap the current model for a smaller, cheaper model to lower the per-call cost
D) Introduce a response cache (e.g., Redis) keyed on normalized query text with a reasonable TTL, so repeated or near-duplicate questions are served from cache instead of re-invoking the LLM

---

**Q40.** You're three minutes into a live demo to the client's C-suite when the RAG system returns a visibly hallucinated output on a slide the CFO is scrutinizing closely. What is the BEST immediate action?

A) Stop the demo entirely and reschedule for another day
B) Ignore it and hope no one else notices, continuing with the script as planned
C) Acknowledge the anomaly briefly, pivot to a pre-recorded backup of that exact scenario, and continue — addressing the root cause afterward
D) Restart the demo from the very beginning to avoid confusion

---

**Q41.** During discovery, you find the VP of Engineering enthusiastic and vocal about the solution, but the actual purchase decision requires sign-off from a CFO who has never attended a single meeting or been named in any conversation. This gap represents a failure to identify which stakeholder role?

A) Economic buyer
B) Technical champion
C) Coach
D) End user

---

**Q42.** Which of the following is the MOST common reason a technically successful PoC fails to secure budget approval to advance into an MVP?

A) The PoC took longer than four weeks to complete
B) The PoC was built using open-source tools instead of proprietary licensed software
C) The PoC was demoed to the technical team before the business team
D) The PoC report focused on technical validation without quantifying business impact against the originally agreed success criteria

---

**Q43.** During a solution scoping workshop, you need to establish quantifiable success metrics for a document-processing AI agent PoC before build begins. Which combination of metrics BEST anchors the eventual ROI conversation with the business sponsor?

A) Model accuracy score and number of GPUs used
B) Number of lines of code written and sprint velocity
C) Baseline manual-processing time/cost and a target automation rate tied to a dollar-value reduction
D) User satisfaction survey results collected six months after go-live only

---

**Q44.** In the Problem-Insight-Solution-Impact demo narrative arc, what is the primary purpose of the 'Insight' stage that sits between Problem and Solution?

A) To reveal a non-obvious root cause or pattern in the client's own data or process that reframes the problem and builds urgency before the solution is presented
B) To showcase the technical architecture diagram of the proposed solution
C) To list competitor products that fail to adequately solve the stated problem
D) To provide pricing and licensing details ahead of the solution reveal

---

**Q45.** Two weeks after a production AI agent went live, it begins producing incorrect outputs that affect the client's downstream billing system. The client's ops team escalates urgently. As the FDE acting in a trusted-advisor role, what is the BEST first step per crisis management protocol?

A) Immediately push a fix to production without informing the client, to resolve the issue as quickly as possible
B) Wait until the root cause is fully identified before saying anything to the client, to avoid looking incompetent
C) Redirect the client to the standard support ticketing system and let the on-call engineer handle it without any advisor-level communication
D) Acknowledge the issue to the client within the agreed SLA window, communicate an immediate rollback or mitigation plan, and open a transparent incident channel before full root-causing is complete

---

