<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:6366F1,100:22D3EE&height=200&section=header&text=Shamika%20Keshan&fontSize=42&fontColor=fff&animation=fadeIn&fontAlignY=35&desc=Software%20Engineer%20%E2%80%A2%20Backend%20%E2%80%A2%20Full%20Stack%20%E2%80%A2%20Cloud%20%26%20DevOps&descAlignY=55" width="100%" alt="Shamika Keshan — Software Engineer"/>

<a href="https://github.com/keshan-dev">
  <img src="https://readme-typing-svg.demolab.com/?lines=Backend+systems+that+stay+correct+when+things+fail;Java+%C2%B7+Spring+Boot+%C2%B7+Python+%C2%B7+FastAPI+%C2%B7+Go+%C2%B7+React;Event-driven+services+with+Kafka%2C+Saga+%26+Outbox;Secure%2C+tested+and+observable+%E2%80%94+end+to+end&font=Fira+Code&size=20&pause=1500&color=22D3EE&center=true&width=700&height=40" alt="Typing summary of skills" />
</a>

<br/>

[![Portfolio](https://img.shields.io/badge/Portfolio-keshan--dev.github.io-000000?style=flat-square&logo=githubpages&logoColor=white)](https://keshan-dev.github.io)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-shamika--keshan-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shamika-keshan)
[![Email](https://img.shields.io/badge/Email-justkeshan%40gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:justkeshan@gmail.com)
![Open to work](https://img.shields.io/badge/Open_to-Software_Engineering_Internships-22C55E?style=flat-square)

</div>

<br/>

## About Me

I'm a Software Engineering undergraduate at **NSBM Green University** who builds software **end to end**: database schema, REST APIs, security, frontend, automated tests, containers and monitoring. Then I try to break it to see what holds.

My projects focus on what production systems actually need: **data that stays consistent when services fail**, **APIs that are secure by default**, and **performance changes backed by measurement**, not guesses.

- 🎯 Looking for **Software Engineering internships** (full-stack, backend or platform). Based in Sri Lanka, open to hybrid and remote
- ⚙️ Strongest in **Java + Spring Boot**, **Python + FastAPI** and **React**, with hands-on **Go**, **Kafka**, **Docker** and **Terraform**
- 🧠 Strong Java problem-solving from a competitive programming background

<br/>

## What I Bring to a Team

| Capability | Where I've shown it |
|:--|:--|
| 🔁 **Ship features end to end** | **Silverline:** Flyway schema → Spring Boot API → JWT/RBAC → React UI → API and security tests |
| 🧱 **Keep data correct under failure** | **OrderFlow:** Saga with compensation, transactional outbox, idempotent consumers, retry and dead-letter topics |
| ⚡ **Improve performance with evidence** | **Silverline:** composite indexes, N+1 queries removed, database-level pagination, Caffeine caching, slow side effects moved to `@Async` |
| 🔐 **Build security in from the start** | JWT + RBAC, GitHub/Atlassian OAuth with multi-tenancy, HMAC-signed requests with replay protection, zero-trust workload identity |
| ✅ **Prove it works** | 550+ tests (HeadRef), 52 tests (DevOps Command Center), Spring test slices, k6 load tests and chaos testing (OrderFlow) |
| ☁️ **Deploy and observe it** | Docker, Terraform, AWS CDK, GitHub Actions, Prometheus, Alertmanager and Loki |
| 🤖 **Use AI responsibly** | **HeadRef:** rules produce every finding, the LLM only writes the summary, and a validator rejects any claim without a real source |

<br/>

## Featured Projects

### 🧾 Silverline: Retail Operations Control System

A full-stack retail system with **admin, manager and POS interfaces** running on a secured Spring Boot API.

- **Business workflows:** built the Goods Received Note workflow that replaced the item-dispatch module, plus per-branch pricing and batch-level pricing with stackable promotions
- **Security:** JWT authentication and role-based access control with Spring Security, request rate limiting and request tracing
- **Performance:** composite indexes on high-traffic queries, removed N+1 queries with `@EntityGraph`, database-level pagination, and Caffeine caching for read-heavy reference data. Audit logging, email and WebSocket broadcasts run `@Async`, outside the request path
- **Frontend:** React admin, manager and POS apps built from feature-based modules with React Query
- **Quality:** schema changes managed with Flyway; Spring MVC and Spring Security test slices cover the REST API and RBAC rules

`Java` `Spring Boot` `Spring Security` `JWT` `PostgreSQL` `Flyway` `React` `React Query`

[![Backend](https://img.shields.io/badge/Backend_Repo-181717?style=flat-square&logo=github)](https://github.com/silverline-pos-system/springboot-be)
[![Frontend](https://img.shields.io/badge/Frontend_Repo-181717?style=flat-square&logo=github)](https://github.com/silverline-pos-system/react-fe)

---

### 📦 OrderFlow: Event-Driven Order Platform · *personal project, ongoing*

Five services (Python and Go) that save an order, reserve stock, take payment and confirm it, or **undo every step** when something fails. It is built to stay correct when services crash, messages arrive twice or the payment provider is slow.

```mermaid
flowchart LR
    C(["Client"]) --> LB["nginx<br/>load balancer"]
    LB --> O["order-service<br/>FastAPI · saga orchestrator"]
    O -->|"same transaction"| ODB[("orders_db<br/>+ outbox")]
    ODB -.->|"Debezium CDC"| K{{"Kafka"}}
    K <--> INV["inventory-service<br/>FastAPI"]
    INV --> R[("Redis<br/>Lua stock holds")]
    K <--> PAY["payment-service<br/>Go"]
    K --> SI["search-indexer"] --> OS[("OpenSearch")]
    O --> MQ{{"RabbitMQ"}} --> NW["notification-worker"] --> S3[("S3<br/>PDF invoices")]
```

- **Saga orchestration:** the order service runs a state machine through stock reservation and payment, with compensation (stock release and refunds) when a step fails or times out
- **Reliable events:** a transactional outbox (Debezium to Kafka) means "data saved" and "event sent" can never disagree. Idempotent consumers, retry and dead-letter topics make duplicate events harmless, and an `Idempotency-Key` stops a retried request from creating a second order
- **Stock and payments:** atomic stock reservation with Redis Lua scripts, PostgreSQL for inventory persistence, payment service written in Go. Each service owns its own database
- **Measured, not assumed** ([raw results](https://github.com/keshan-dev/orderflow/tree/main/results/phase-1)):

| Test (k6) | Result |
|:--|:--|
| Search during a zero-downtime OpenSearch reindex | **7,032 requests, 0 failed**, p95 76.9 ms |
| Killing an API instance behind nginx | **6,175 requests, 0 failed** |
| Load + chaos round 1 (random service kills) | Found **2 consistency bugs**; fixes in progress |

`Python` `FastAPI` `Go` `PostgreSQL` `Kafka` `Debezium` `RabbitMQ` `Redis` `OpenSearch` `nginx` `Docker` `k6`

[![Repo](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github)](https://github.com/keshan-dev/orderflow)

---

### 🔎 HeadRef: Evidence-Linked Team Insight Tool

Reads GitHub and Jira and tells a team lead **what each person is working on, what's blocking them and what's at risk**. Every statement links to the record it came from.

- **Data sync and linking:** FastAPI integration pulls data from GitHub and Jira, syncs it into PostgreSQL with Alembic migrations, and links Jira issues to their branches, pull requests and commits
- **Validated LLM pipeline:** deterministic rules produce every finding and a local Ollama model writes only the summary. A validator rejects unsupported claims, so each statement cites a real source record
- **Security:** GitHub App and Atlassian OAuth with multi-tenant workspaces, role-based access and read-only scopes
- **Testing:** 550+ tests, including checks that no secret ever reaches the model prompt

`Python` `FastAPI` `PostgreSQL` `SQLAlchemy` `Alembic` `Ollama` `OAuth` `GitHub Actions` `pytest`

[![Repo](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github)](https://github.com/c-clarke-group-projects/headref)

---

### 🏦 Arka: Cell-Isolated Digital Banking Platform · *Duothan 6.0 buildathon*

A digital banking platform split into **isolated Cells that share no network path**, built by a team; my scope is below.

- **Zero-trust foundation:** shared service contracts, short-lived workload-identity authentication and the API gateway Cell Router, so every service-to-service call proves its identity
- **Identity and recovery:** identity service with multi-layered authentication, plus an operator Recovery Console with live Cell health, dual-approval quarantine and an audit trail
- **Ledger integrity:** hash-chained integrity audit with export, so tampering with the double-entry ledger is detectable
- **Infrastructure as code:** AWS CDK and Terraform for per-Cell VPCs

`TypeScript` `Node.js` `PostgreSQL` `Redis Streams` `AWS CDK` `Terraform` `GitHub Actions`

[![Repo](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github)](https://github.com/keshan-dev/arka)

---

### 📟 AI-Powered Mobile DevOps Command Center · *university group project*

Detects incidents in running services and triggers **safe, automated recovery playbooks**.

- **Monitoring and alerting:** Prometheus, Alertmanager, Loki and Promtail stack with error-rate and service-down alerts (covered by rule unit tests), delivered to n8n through a token-protected webhook
- **Secure playbook executor:** Python service that runs restart and circuit-breaker playbooks only from HMAC-signed requests. It rejects replayed requests, runs each playbook at most once and acts only on allow-listed services
- **Fault injection and testing:** FastAPI sample service with metrics, JSON logs, switchable faults and a load generator for the end-to-end demo, plus 52 tests across the executor and sample app

`Python` `FastAPI` `Prometheus` `Alertmanager` `Loki` `Promtail` `n8n` `Docker` `pytest`

<br/>

## Engineering Fundamentals

| Area | What I know | Applied in |
|:--|:--|:--|
| **Programming** | OOP, classes, interfaces, collections, exception handling | Spring Boot services in Silverline |
| **Data structures and algorithms** | Arrays, linked lists, stacks, queues, hash maps, searching, sorting | Competitive programming in Java |
| **Software design** | SOLID, dependency injection, Saga, transactional outbox, idempotent consumers | Silverline (Spring DI), OrderFlow |
| **APIs** | REST principles, request validation, authentication and authorization | Every project above |
| **Databases** | Relational design, joins, normalization, indexing, transactions, ACID; NoSQL with Redis and OpenSearch | Silverline indexing, OrderFlow outbox and Lua scripts |
| **Distributed systems** | Retries, timeouts, dead-letter queues, compensation, rate limiting, failover | OrderFlow |
| **Software quality** | Unit and integration testing, debugging, Git, CI/CD | HeadRef (550+ tests), Silverline test slices |

<br/>

## Tech Stack

| | |
|:--|:--|
| **Languages** | <img src="https://skillicons.dev/icons?i=java,py,ts,js,go" alt="Java, Python, TypeScript, JavaScript, Go" /><br/><img src="https://img.shields.io/badge/SQL-336791?style=flat-square&logo=postgresql&logoColor=white" alt="SQL" /> |
| **Backend** | <img src="https://skillicons.dev/icons?i=spring,fastapi,nodejs" alt="Spring Boot, FastAPI, Node.js" /><br/><img src="https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white" alt="Spring Security" /> <img src="https://img.shields.io/badge/REST_APIs-0A0A0A?style=flat-square" alt="REST APIs" /> <img src="https://img.shields.io/badge/JWT-000000?style=flat-square&logo=jsonwebtokens&logoColor=white" alt="JWT" /> |
| **Frontend** | <img src="https://skillicons.dev/icons?i=react" alt="React" /><br/><img src="https://img.shields.io/badge/React_Query-FF4154?style=flat-square&logo=reactquery&logoColor=white" alt="React Query" /> |
| **Databases, Messaging and Search** | <img src="https://skillicons.dev/icons?i=postgres,mysql,redis,kafka,rabbitmq" alt="PostgreSQL, MySQL, Redis, Kafka, RabbitMQ" /><br/><img src="https://img.shields.io/badge/OpenSearch-005EB8?style=flat-square&logo=opensearch&logoColor=white" alt="OpenSearch" /> <img src="https://img.shields.io/badge/Debezium-91D443?style=flat-square" alt="Debezium" /> |
| **Cloud, DevOps and Observability** | <img src="https://skillicons.dev/icons?i=aws,terraform,docker,linux,nginx,githubactions,git,prometheus" alt="AWS, Terraform, Docker, Linux, nginx, GitHub Actions, Git, Prometheus" /><br/><img src="https://img.shields.io/badge/Loki-F46800?style=flat-square&logo=grafana&logoColor=white" alt="Loki" /> |
| **AI and Automation** | <img src="https://img.shields.io/badge/Ollama-000000?style=flat-square&logo=ollama&logoColor=white" alt="Ollama" /> <img src="https://img.shields.io/badge/LLM_APIs-6366F1?style=flat-square" alt="LLM APIs" /> <img src="https://img.shields.io/badge/n8n-EA4B71?style=flat-square&logo=n8n&logoColor=white" alt="n8n" /> |
| **Testing** | <img src="https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white" alt="pytest" /> <img src="https://img.shields.io/badge/Spring_Test-6DB33F?style=flat-square&logo=spring&logoColor=white" alt="Spring Test" /> <img src="https://img.shields.io/badge/k6-7D64FF?style=flat-square&logo=k6&logoColor=white" alt="k6" /> |

<br/>

## Currently Building

- ☸️ **OrderFlow, next phase:** shipping it to Kubernetes with GitOps, and adding OpenTelemetry tracing with Prometheus, Loki, Jaeger and Grafana
- 🛠️ **After that:** a Kubernetes operator in Go, an eBPF runtime security agent, and running the full platform on AWS with Terraform
- 🤖 **AI engineering:** RAG pipelines, FastAPI services and n8n automation

<br/>


## GitHub Stats

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=keshan-dev&show_icons=true&theme=tokyonight&hide_border=true&count_private=true" height="165" alt="GitHub stats" />
<img src="https://streak-stats.demolab.com/?user=keshan-dev&theme=tokyonight&hide_border=true" height="165" alt="GitHub streak" />

</div>

<br/>

<div align="center">

**Hiring a software engineering intern?** I'd be glad to talk: [justkeshan@gmail.com](mailto:justkeshan@gmail.com) · [LinkedIn](https://www.linkedin.com/in/shamika-keshan)

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:22D3EE,100:6366F1&height=120&section=footer" width="100%" alt=""/>

</div>