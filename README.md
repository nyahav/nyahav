<h1 align="center">Hi 👋, I'm Yahav Nir</h1>
<h3 align="center">Backend Engineer specializing in secure, scalable architecture, distributed microservices, and performance optimization.</h3>
<img align="right" alt="Coding" width="400" src="https://media1.tenor.com/m/2fXbn6Xtt0UAAAAC/software-software-development.gif">

<p align="left"> <img src="https://komarev.com/ghpvc/?username=nyahav&label=Profile%20views&color=0e75b6&style=flat" alt="nyahav" /> </p>

<h3 align="left">Connect with me:</h3>
<p align="left">
<a href="https://www.linkedin.com/in/nir-yahav" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="nyahav" height="30" width="40" /></a>
<a href="mailto:yahavnirr@gmail.com" target="blank"><img align="center" src="https://img.shields.io/badge/Email%20%2F%20Copy-yahavnirr%40gmail.com-D14836?style=flat&logo=gmail&logoColor=white" alt="Email" height="30" style="margin-left: 10px;" /></a>
</p>

<h3 align="left">Languages and Tools:</h3>
<a href="https://www.java.com/" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" alt="java" width="40" height="40"/> 
</a>
<a href="https://www.python.org/" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> 
</a>
<a href="https://www.typescriptlang.org/" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/typescript/typescript-original.svg" alt="typescript" width="40" height="40"/> 
</a>
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript" width="40" height="40"/> 
</a>
<a href="https://nodejs.org" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nodejs/nodejs-original-wordmark.svg" alt="nodejs" width="40" height="40"/> 
</a>
<a href="https://www.postgresql.org/" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/postgresql/postgresql-original-wordmark.svg" alt="postgresql" width="40" height="40"/> 
</a>
<a href="https://www.mongodb.com/" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg" alt="mongodb" width="40" height="40"/> 
</a>
<a href="https://www.docker.com/" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original-wordmark.svg" alt="docker" width="40" height="40"/> 
</a>
<a href="https://reactjs.org/" target="_blank" rel="noreferrer"> 
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original-wordmark.svg" alt="react" width="40" height="40"/> 
</a>

## 🛠️ Engineering Deep Dive: Designing a Highly Available Resource-Manager Service

Instead of just listing my skills, I prefer to share how I apply them to solve production challenges. 
Below is a breakdown of a core architectural problem I owned and resolved.

### 🛑 The Challenge
A distributed orchestration system processing heavy analytical tools suffered from severe scalability bottlenecks and stability issues under peak traffic:
* **Throughput Constraints:** The system experienced massive task processing delays due to unoptimized scheduling logic.
* **Scheduling Latency:** Fetching and evaluating task states constantly against the database introduced a **200ms latency** per scheduling cycle.
* **System Crashes:** Sudden spikes in high-memory tools led to unpredictable Out-of-Memory (OOM) crashes across worker nodes, bringing down the cluster.

---

### 🏗️ Architectural Evaluation & Decision Matrix

To solve this, I evaluated three potential approaches for task scheduling and system protection:

| Feature | Option A: Distributed Locking (DB-centric) | Option B: Standard Message Queueing (FIFO) | Option C: Custom Weighted Scheduler + 2-Tier Admission Controller (Chosen) |
| :--- | :--- | :--- | :--- |
| **Throughput** | Low (DB Bottleneck) | Medium (No resource awareness) | **High (Tailored resource allocation)** |
| **Latency** | High (>200ms) | Low (<10ms) | **Ultra-Low (~5ms using In-Memory Cache)** |
| **OOM Protection** | None (Reactive) | Weak (Static rate limiting) | **Proactive (Priority-based preemption)** |

* **Why Option C?** Traditional FIFO queues couldn't differentiate between a light script and a heavy analytical task, leading to resource starvation. A custom weighted scheduler coupled with reactive admission controls allowed us to maximize CPU/Memory utilization safely without crashing nodes.

---

### 💻 The Implementation

I engineered a custom orchestration component utilizing **Java/Kotlin**, **RabbitMQ**, and an **in-memory caching layer**:

1. **Custom Weighted Scheduler:** Implemented an algorithm that scores incoming tasks based on priority, historical execution data, and real-time node capacity. To bypass the DB latency, I moved active scheduler states into a highly optimized, thread-safe in-memory cache.
2. **Two-Tier Admission Controller:** Built a defensive layer that intercepts tasks before execution. Tier 1 checks global cluster health. Tier 2 handles **priority-based preemption**—if a critical task arrives and memory is tight, low-priority tasks are gracefully paused/re-queued.
3. **Automated Recovery:** Developed an asynchronous Watchdog system that monitors worker heartbeats and automatically triggers crash-recovery and state-reconciliation routines if a node fails.

---

### 📊 The Impact (Production Results)

* **3x Increase in Tool Throughput:** Optimized resource utilization allowed the cluster to run three times more tasks concurrently.
* **Latency Slashed by 97.5%:** Scheduling cycle latency dropped from **200ms to just 5ms**.
* **90% Reduction in OOM Crashes:** Proactive admission control completely stabilized the cluster under peak loads.

---

## 🔒 Core Expertise 
* **Backend Architecture:** Microservices, Event-Driven Systems, System Integration.
* **Security First:** Identity Management, Centralized Auth (Keycloak, OAuth2, PKCE).
* **Data Engineering:** Hybrid SQL/NoSQL migrations, Query Optimization, High-Volume Data Pipelines.
* **Infrastructure:** Containerization (Docker), Enterprise Messaging (RabbitMQ), High-Availability Systems.
