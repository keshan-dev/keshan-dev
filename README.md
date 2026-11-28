<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:6366F1,100:22D3EE&height=200&section=header&text=Shamika%20Keshan&fontSize=42&fontColor=fff&animation=fadeIn&fontAlignY=35&desc=System%20Design%20%E2%80%A2%20Full%20Stack%20%E2%80%A2%20AI%20Integration%20%E2%80%A2%20Cloud&descAlignY=55" width="100%"/>

<a href="https://github.com/keshan-dev">
  <img src="https://readme-typing-svg.demolab.com/?lines=Designing+systems+that+survive+failure;Full+stack%3A+Spring+Boot+%C2%B7+FastAPI+%C2%B7+React;Integrating+LLMs+that+cite+their+sources;Shipping+to+the+cloud+with+Docker+%26+Terraform&font=Fira+Code&size=20&pause=1500&color=22D3EE&center=true&width=650&height=40" />
</a>

<br/>

[![Portfolio](https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=githubpages&logoColor=white)](https://keshan-dev.github.io)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shamika-keshan)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:justkeshan@gmail.com)

![Open to Internships](https://img.shields.io/badge/🟢_Open_to-Software_Engineering_Internships-22C55E?style=flat-square)

</div>

<br/>

## 👋 About Me

Software Engineering undergraduate at **NSBM Green University**. I design and build systems **end to end**, from architecture and APIs to AI features and cloud deployment.

<br/>

## 🎯 What I Do

<table>
<tr>
<td width="50%" valign="top">

### 🏗️ System Design
Distributed systems that stay correct under failure.

- Saga orchestration · Transactional outbox · CDC
- Idempotency · Retries · Dead-letter queues
- Caching · Rate limiting · Load balancing
- Cell-based isolation · Zero-trust identity

</td>
<td width="50%" valign="top">

### 💻 Full Stack
Secure, fast products from database to UI.

- REST APIs with **Spring Boot**, **FastAPI**, **Node.js**
- **React** frontends with React Query
- JWT · RBAC · OAuth · Multi-tenancy
- Indexing · N+1 fixes · Migrations

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🤖 AI Integration
LLM features you can trust in production.

- Local LLMs with **Ollama** + LLM APIs
- Rule-based findings, LLM-written summaries
- Output validation: every claim cites a source
- Workflow automation with **n8n**

</td>
<td width="50%" valign="top">

### ☁️ Cloud & DevOps
Infrastructure as code, monitored and automated.

- **AWS** with **CDK** + **Terraform**
- **Docker** · **GitHub Actions** CI/CD
- **Prometheus** · Alertmanager · **Loki**
- Load and chaos testing with **k6**

</td>
</tr>
</table>

<br/>

## 🧰 Tech Stack

<div align="center">

| | |
|:--:|:--|
| **Languages** | <img src="https://skillicons.dev/icons?i=java,py,ts,js,go" /> |
| **Full Stack** | <img src="https://skillicons.dev/icons?i=spring,fastapi,nodejs,react" /> |
| **Data & Messaging** | <img src="https://skillicons.dev/icons?i=postgres,mysql,redis,kafka,rabbitmq" /> |
| **Cloud & DevOps** | <img src="https://skillicons.dev/icons?i=aws,terraform,docker,nginx,githubactions,prometheus,linux" /> |
| **AI & Automation** | ![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white) ![LLM APIs](https://img.shields.io/badge/LLM_APIs-6366F1?style=for-the-badge) ![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white) |

</div>

<br/>

## 🧩 System Design Spotlight: OrderFlow

```mermaid
flowchart LR
    C(["Client"]) --> LB["nginx<br/>load balancer"]
    LB --> O["order-service<br/>saga orchestrator"]
    O -->|"same transaction"| ODB[("orders_db<br/>+ outbox")]
    ODB -.->|"Debezium CDC"| K{{"Kafka"}}
    K <--> INV["inventory-service"]
    INV --> R[("Redis<br/>atomic stock")]
    K <--> PAY["payment-service<br/>Go"]
    K --> SI["search-indexer"] --> OS[("OpenSearch")]
    O --> MQ{{"RabbitMQ"}} --> NW["notification-worker"] --> S3[("S3")]
```

<div align="center">

![Requests](https://img.shields.io/badge/Failover_test-6,175_requests_·_0_failed-22C55E?style=flat-square)
![Reindex](https://img.shields.io/badge/Zero--downtime_reindex-7,032_requests_·_0_failed-22C55E?style=flat-square)

</div>

<br/>

## 🚀 Featured Projects

<table>
<tr>
<td width="50%" valign="top">

### 📦 OrderFlow
![](https://img.shields.io/badge/System_Design-6366F1?style=flat-square) ![](https://img.shields.io/badge/Cloud-0EA5E9?style=flat-square)

**Event-driven order platform**, 5 services in Python + Go.

✅ Saga + outbox + idempotent consumers<br/>
✅ Redis Lua atomic stock reservation<br/>
✅ Load and chaos tested with k6

[![Repo](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github)](https://github.com/keshan-dev/orderflow)

</td>
<td width="50%" valign="top">

### 🧾 Silverline
![](https://img.shields.io/badge/Full_Stack-22C55E?style=flat-square) ![](https://img.shields.io/badge/System_Design-6366F1?style=flat-square)

**Retail operations system** with admin, manager and POS apps.

✅ Spring Boot API + React frontend<br/>
✅ JWT + RBAC, rate limiting, tracing<br/>
✅ Indexing, caching, async processing

[![Backend](https://img.shields.io/badge/Backend-181717?style=flat-square&logo=github)](https://github.com/silverline-pos-system/springboot-be)
[![Frontend](https://img.shields.io/badge/Frontend-181717?style=flat-square&logo=github)](https://github.com/silverline-pos-system/react-fe)

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🔎 HeadRef
![](https://img.shields.io/badge/AI_Integration-EC4899?style=flat-square) ![](https://img.shields.io/badge/Full_Stack-22C55E?style=flat-square)

**AI team insight tool** on GitHub + Jira data.

✅ Validated LLM pipeline with Ollama<br/>
✅ Every claim linked to a real source<br/>
✅ OAuth, multi-tenant, 550+ tests

[![Repo](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github)](https://github.com/c-clarke-group-projects/headref)

</td>
<td width="50%" valign="top">

### 🏦 Arka
![](https://img.shields.io/badge/Cloud-0EA5E9?style=flat-square) ![](https://img.shields.io/badge/System_Design-6366F1?style=flat-square)

**Cell-isolated banking platform** · Duothan 6.0 buildathon.

✅ Per-Cell AWS VPCs with CDK + Terraform<br/>
✅ Zero-trust service identity<br/>
✅ Tamper-evident ledger audit

[![Repo](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github)](https://github.com/keshan-dev/arka)

</td>
</tr>
<tr>
<td colspan="2" valign="top">

### 📟 AI-Powered DevOps Command Center
![](https://img.shields.io/badge/AI_Integration-EC4899?style=flat-square) ![](https://img.shields.io/badge/Cloud-0EA5E9?style=flat-square)

**Automated incident detection and recovery** · university group project.

✅ Prometheus + Loki alerts into n8n &nbsp;&nbsp; ✅ HMAC-signed recovery playbooks &nbsp;&nbsp; ✅ Fault injection + 52 tests

</td>
</tr>
</table>

<br/>

## 📊 GitHub Stats

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=keshan-dev&show_icons=true&theme=tokyonight&hide_border=true&count_private=true" height="165" />
<img src="https://streak-stats.demolab.com/?user=keshan-dev&theme=tokyonight&hide_border=true" height="165" />

</div>

<br/>

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:22D3EE,100:6366F1&height=120&section=footer" width="100%"/>

</div>