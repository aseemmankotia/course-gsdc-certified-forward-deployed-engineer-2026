## Chapter 9: Rapid Prototyping UI and Cloud Deployment — Practice Questions

**Q1.** A data science team built a quick internal demo to showcase a fine-tuned image classification model. Stakeholders need to drag-and-drop images and instantly see predicted labels with confidence scores, with minimal front-end code. Which tool BEST fits this requirement?

A) Gradio with gr.Interface using an Image input and Label output component
B) Streamlit with a custom file_uploader and matplotlib chart
C) A hand-built Flask app with HTML forms
D) Django with a REST API and a separate React frontend

<details>
<summary>Answer</summary>

**Correct: A**

Gradio's gr.Interface auto-generates upload widgets and prediction displays for ML I/O types (Image, Label) in a few lines, making it the fastest path for model-centric demos.

**Why the others are wrong:**
- Streamlit is better suited for multi-page dashboards and data apps, not the fastest option for a single model I/O demo
- Flask requires building the entire UI manually, far slower than a declarative interface
- Django + React is a full production stack, massive overkill for a quick internal demo

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A developer accidentally commits an OpenAI API key to a public GitHub repository. The commit has already been pushed and merged. What is the BEST immediate response?

A) Delete the file containing the key in a new commit
B) Make the repository private so the key is no longer visible
C) Revoke/rotate the exposed key immediately, then remove it from git history and add it to .gitignore
D) Add a .env file with the key going forward and leave the old commit as-is

<details>
<summary>Answer</summary>

**Correct: C**

Deleting the file in a new commit does not remove the key from git history; the key must be treated as compromised and revoked/rotated first, then purged from history (e.g., git filter-repo) and prevented from re-entry.

**Why the others are wrong:**
- The key remains readable in prior commits in the full git history even after deletion
- Making the repo private doesn't invalidate a key already scraped by bots that continuously scan public commits
- Leaving the old commit means the compromised key is still valid and exploitable

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A team's Docker image for their AI inference app is 4.2GB because it includes the full build toolchain (compilers, dev headers) used only to build a Python wheel. What is the BEST way to reduce image size for production?

A) Switch the base image from python:3.12 to python:3.12-slim only
B) Add more RUN apt-get clean commands after each install
C) Use a multi-stage Dockerfile: build the wheel in a builder stage, then copy only the compiled artifacts into a minimal final stage
D) Compress the final image using a zip archive before pushing to the registry

<details>
<summary>Answer</summary>

**Correct: C**

Multi-stage builds separate build-time dependencies from runtime, discarding compilers and dev headers entirely in the final image layer.

**Why the others are wrong:**
- Switching base images helps but doesn't remove build tools already installed via RUN commands in a single-stage build
- apt-get clean reduces cache but the toolchain packages themselves remain installed and consume space
- Docker images aren't distributed as zip archives; registries store layered images, not compressed files

</details>

---

**Q4.** An AI application running on AWS ECS needs to retrieve a database password and third-party API key at container startup, with support for automatic rotation. Which AWS service should be used?

A) AWS Secrets Manager
B) Hardcode the credentials as environment variables in the task definition
C) Store the credentials in a public S3 bucket for easy access
D) Bake the credentials into the Docker image at build time

<details>
<summary>Answer</summary>

**Correct: A**

AWS Secrets Manager supports encrypted storage, IAM-scoped access, and automatic rotation of database/API credentials, integrating directly with ECS task definitions.

**Why the others are wrong:**
- Plaintext env vars in task definitions are visible to anyone with describe-task-definition permissions and don't support rotation
- Public S3 buckets expose secrets to the internet, a critical security failure
- Baking credentials into an image means anyone who pulls the image has the secret permanently, and rotation requires rebuilding/redeploying

</details>

---

**Q5.** A company wants to deploy the same containerized AI inference service with automatic scale-to-zero on GCP to minimize idle cost. Which service should they use?

A) GCP Compute Engine with a fixed VM instance group
B) GCP Kubernetes Engine (GKE) with manually managed nodes
C) GCP App Engine Standard with always-on instances
D) GCP Cloud Run

<details>
<summary>Answer</summary>

**Correct: D**

Cloud Run is GCP's fully managed serverless container platform that scales to zero when idle and scales up automatically on request, directly analogous to AWS Fargate/Azure Container Apps.

**Why the others are wrong:**
- Compute Engine VMs run continuously and incur cost even when idle unless manually stopped
- GKE with manually managed nodes requires cluster/node management and doesn't scale to zero by default
- App Engine Standard 'always-on' instances are explicitly configured to avoid cold starts, defeating the scale-to-zero cost goal

</details>

---

**Q6.** A Streamlit app loads a large embedding model and opens a persistent connection object that cannot be pickled. Which caching decorator should be used to avoid reloading it on every rerun?

A) @st.cache_data
B) @st.cache_resource
C) @st.session_state
D) @st.memo

<details>
<summary>Answer</summary>

**Correct: B**

@st.cache_resource is designed for non-serializable, shared objects like ML models and database connections, storing a single instance across reruns and sessions.

**Why the others are wrong:**
- @st.cache_data serializes and copies return values, which fails or is inappropriate for unpicklable objects like open connections
- st.session_state is a per-session dictionary, not a caching decorator, and reinitializes per session rather than sharing across all users
- @st.memo is not a real Streamlit decorator

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** To maximize Docker build cache hits and speed up rebuilds for a Python AI app, which Dockerfile instruction order is BEST?

A) COPY . . followed by RUN pip install -r requirements.txt
B) RUN pip install -r requirements.txt before any COPY instruction
C) COPY requirements.txt . then RUN pip install -r requirements.txt, then COPY . .
D) Combine all COPY and RUN pip install into a single RUN line at the end

<details>
<summary>Answer</summary>

**Correct: C**

Copying requirements.txt first and installing dependencies before copying the rest of the source code lets Docker reuse the cached dependency layer whenever only application code changes, since that layer's checksum is unaffected.

**Why the others are wrong:**
- Copying the entire source tree before installing dependencies invalidates the pip install cache layer on every code change, even trivial ones
- Running pip install with no requirements file copied yet would fail since the file doesn't exist in the build context
- Combining everything into one RUN/COPY line prevents Docker from caching any intermediate layer, forcing full reinstall on any change

</details>

---

**Q8.** An AI application calling an external LLM API begins receiving HTTP 429 responses under load. What is the standard client-side pattern to handle this correctly?

A) Immediately retry the request in a tight loop until it succeeds
B) Switch to a synchronous blocking call to guarantee delivery
C) Catch the 429, wait using exponential backoff (with jitter), and retry up to a bounded number of attempts
D) Ignore the error and drop the request silently

<details>
<summary>Answer</summary>

**Correct: C**

429 (Too Many Requests) signals rate limiting; the correct client pattern is exponential backoff with jitter and a retry cap to avoid overwhelming the API further while still recovering gracefully.

**Why the others are wrong:**
- Tight-loop retries amplify load on the already-throttled endpoint and can trigger longer bans or account suspension
- Switching to synchronous calls has no effect on rate limits; sync vs async is unrelated to whether the request rate exceeds quota
- Silently dropping requests causes data loss and unpredictable application behavior with no recovery path

</details>

---

