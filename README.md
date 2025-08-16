# CST8917_Assignment2

# CST8917 – Serverless Service Alternatives Report

**Due:** Week 15 (August 15, 2025) — Submit GitHub repository link via Brightspace by 11:59 PM  
**Weight:** 10% • **Type:** Individual Assignment

## 🎯 Objective
This report will show the Azure serverless services taken during the course and compare it with the most similar alternative in Amazon Web Services (AWS) and in Google Cloud Platform (GCP). Each service will have: **Overview**, **Core Features (triggers/bindings/eventing)**, **Integration Options**, **Monitoring & Observability**, **Pricing Model (high-level)** and **Strengths & Weaknesses**. The point is to assist you to select the proper service according to the amount of work to be done and without much time consumption.

> ⚠️ Ppricing and restrictions vary often. Consider any notes regarding pricing as directional and refer to the linked official pricing pages in preparing a cost estimate.

---

## 🗺️ Quick Cross‑Cloud Map

| Azure (Focus) | AWS Equivalent | GCP Equivalent | Notes |
|---|---|---|---|
| **Azure Functions** | **AWS Lambda** | **Cloud Functions (2nd gen)** (built on Cloud Run + Eventarc) | FaaS in all three clouds Event-driven. Azure features the enriched triggers/bindings model; GCP Gen2 is based on Cloud Run infra. |
| **Durable Functions** (function chaining, fan‑out/fan‑in) | **AWS Step Functions** | **Google Cloud Workflows** | Stateful, long-running orchestration. |
| **Azure Logic Apps** | **Step Functions + EventBridge + AppFlow** | **Application Integration (Integration Connectors) + Workflows + Eventarc** | Large connector device systems where hundreds of connectors can be low-coded together. |
| **Service Bus (Queues & Topics)** | **Amazon SQS (queues) + Amazon SNS (topics)** | **Pub/Sub** | Message driven enterprise; FIFO/session capability on Service Bus vs SQS/SNS; Pub/Sub supports topic/subscription semantics. |
| **Event Grid** | **Amazon EventBridge** | **Eventarc** | Filtered and SaaS-integrated event routing / bus. |
| **Event Hubs** | **Amazon Kinesis Data Streams** | **Pub/Sub (streaming ingestion)** | Telemetry/logs/IoT ingestion High throughput ingestion; variable capacity options (TU/shards/on‑demand). |

---

## 1) Azure Functions vs AWS Lambda vs Google Cloud Functions (2nd gen)

### Overview
- **Azure Functions** — Managed, event-driven compute with a triggers and bindings programming model that simplifies I/O (e.g. Service bus, Event hubs, Event grid, Storage, HTTP, timers).
- **AWS Lambda** — Serverless compute capable of executing code after it has been triggered and auto-scaling; natively integrated with numerous AWS services and API Gateway/EventBridge.   
- **Google Cloud Functions (2nd gen)** — Functions based on **Cloud Run** and **Eventarc** and HTTP and event triggers as well as the underlying execution model of Cloud Run. 

### Core features (triggers/bindings)
- **Azure Functions**: The overall number of triggers to be 1 to 1 to a single function; fat *bindings* to input/output (e.g., queue message in -> process -> write to blob).
- **Lambda**: Triggered by numerous sources (API Gateway, S3, DynamoDB streams, SQS/SNS, EventBridge, and so on).
- **GCF (Gen2)**: HTTP, Pub/Sub, Cloud Storage, Audit Logs and so many Eventarc sources.

### Integration options
- **CI/CD**: GitHub Actions/Azure DevOps Azure CodePipeline/CodeBuild, AWS; Cloud Build (GCP)  
- **Service integrations**: Bindings (azure), Service Integrations & EventBridge (aws), Eventarc + Connectors (gcp.) 

### Monitoring & observability
- **Azure**: In‑built Application Insights / Azure Monitor. 
- **AWS**: **CloudWatch** metrics/logs (and X-Ray for trace).  
- **GCP**: **Cloud Logging**/**Cloud Monitoring** in Cloud Run/Functions.

### Pricing model (high‑level)
- **Azure Functions**: Consumption/Flex per-execution + GBs; Premium per vCPU/single-GBs. 
- **AWS Lambda**: On demand + GB‑seconds (included in free tier). 
- **GCF (Gen2)**: Follows Cloud Run functions pricing (invocations+compute). 

### Strengths & weaknesses (serverless lens)
- **Azure Functions**: Strong bindings minimize boilerplate; − tight integrations in Azure; - bindings are tied to an Azure‑specific platform (portability). 
- **AWS Lambda**: + mature environment/ integrations + mature functional tooling – default limits/timeouts may need discussion. 
- **GCF (Gen2)**: + based on Cloud Run - mind increased control and scale; + Eventarc sources; - Gen1/Gen2 differences to watch. 

---

## 2) Durable Functions vs AWS Step Functions vs Google Cloud Workflows

### Overview & patterns
- **Durable Functions** adds stateful orchestrations to Azure Functions (chaining of functions, fan-out/fan-in, human interaction).
- **AWS Step Functions** organizes services, Lambdas and state machines (Standard/Express workflows). 
- **Google Cloud Workflows** coordinates Google Cloud services, HTTP endpoints and Cloud Run/Functions. 

### Integration & developer experience
- Visual designers (Workflow Studio on aws), JSON/YAML setting, retries, branching, error handling, parallel steps. 

### Monitoring & observability
- **Azure**: Orchestration history through Durable runtime + Application Insights. 
- **AWS**: Deployment, Execution history, CloudWatch metrics/logs 
- **GCP**: Raspiyas parMeters in Cloud Logging/Monitoring. 

### Pricing model (high‑level)
- **Durable Functions**: **Same billing as Functions**; be alert to orchestration/storage interplay on Consumption. 
- **Step Functions**: The charge is unusual divided by **state transition** (there are different rates on Standard/Express). 
- **Workflows**: Per step **executed** (first tier free). 

### Strengths & weaknesses
- **Durable**: + Code‑centric in familiar language; − limited to Azure Functions runtime/hosting. 
- **Step Functions**: 200+ service integration, robust patterns; - costs scale with colloquial flows.
- **Workflows**: + Simple YAML and HTTP integrations; - fewer out‑of‑the- box “service integrations” than with AWS. 

---

## 3) Azure Logic Apps vs AWS & GCP iPaaS Options

### Overview
- **Logic Apps**: Built‑in and managed connectors (hundreds of SaaS/enterprise systems) low-code workflows. 
- **Closest AWS fit**: **Step Functions** for where orchestration meets **EventBridge** for where events are and **AppFlow**/**partner connectors** where SaaS data flows 
- **Closest GCP fit**: **Application Integration / Integration Connectors** + **Workflows** + **Eventarc**. 

### Integration options
- Drag-drop designers, hundred’s of out-of-the-box connectors, custom connectors, and HTTP/Webhook support.

### Monitoring & observability
- History, Azure Monitor, diagnostic logs.

### Pricing model (high‑level)
- **Logic Apps**: Consumption (action/connector-based metering) or Standard (FIXED compute units). 
- **AWS**: The costs are based on the services that are triggered (Step Functions transitions, EventBridge events, AppFlow runs). 
- **GCP**: Application Integration and connectors priced on a per-use basis; Workflows/ Eventarc charged on a per step/ event basis. 

### Strengths & weaknesses
- **Logic Apps**: + Very expansive connector library; + hybrid capability; â minus, partial cross- cloud portability due to connector availability.

---

## 4) Service Bus (Queues & Topics) vs SQS/SNS vs Pub/Sub

### Overview
- **Azure Service Bus**: Enterprise broker with queues (competing consumers), topics/subscriptions (pub/sub), sessions when ordered processing is required.  
- **AWS**: **SQS** (queues; standard & FIFO) + **SNS** (topics).  
- **GCP**: Durable pub/sub and streaming ingestion (topics + subscriptions). 

### Integration options
- Увеличенная поддержка распространенных языков (шаблоны для C#, Java, Node.js, Python, Ruby). Triggers/bindings (Azure Functions), Lambda event source mappings (SQS/SNS), Cloud Functions triggers (Pub/Sub). 

### Monitoring & observability
- **Azure**: Service Bus telemetry + Azure Monitor metric/logs. 
- **AWS**: SNS/SQS metrics in CloudWatch.  
- **GCP**: Pub/Sub cloud Monitoring/Logging. 

### Pricing model (high‑level)
- **Service Bus**: Tiered (Basic/Standard/Premium) + message ops; check out the pricing page.  
- **SQS**: Per API request; there are other dimensions of pricing in FIFO.  
- **SNS**: On operation and kind of delivery (HTTP/SQS/Lambda/SMS, and so on).   
- **Pub/Sub**: Throughput (bytes in/out), storage and network egress. 

### Strengths & weaknesses
- **Service Bus**: + Sessions transactons; − premium tier requied for strict latency/acaolation.  
- **SQS/SNS**: + Easy/low cost; - two services to glue to make pub/sub.   
- **Pub/Sub**: Global, scale to many orders of magnitude; + queue-like patterns can require more components. 

---

## 5) Event Grid vs EventBridge vs Eventarc

### Overview
- **Event Grid**: Managment eventing (HTTP + MQTT namespaces) filtering and large number of Azure/system / partner sources.  
- **EventBridge**: SaaS-compatible, incrementally feature-complete replacement of Aurora Serverless with rules, schema registry, SaaS partners, scheduler/Pipes.   
- **Eventarc**: Standard and advanced; global event routing to services GCP and custom events. 

### Monitoring & observability
- **Azure**: Azure Monitor metrics/logs for Event Grid namespaces.  
- **AWS**: EventBridge metrics/alarms in CloudWatch. 
- **GCP**: Eventarc triggers and deliveries Cloud Logging/Monitoring. 

### Pricing model (high‑level)
- **Event Grid**: Pay-per-operation; First free operations/month.
- **EventBridge**: Pay-per-event (plus archive/replay/scheduler where provided). 
- **Eventarc**: Pay per event delivery & features (edition specific). 

### Strengths & weaknesses
- **Event Grid**: Deep Azure source coverage; -not as many third-party SaaS sources as EventBridge. 
- **EventBridge**: + Wide SaaS partners and patterns (rules, Pipes, Scheduler); − cross‑region topologies introduce cost/complexity.  
- **Eventarc**: Native to GCP with Cloud Run/Functions; - requires selection of edition/features

---

## 6) Event Hubs vs Kinesis Data Streams vs Pub/Sub (as streaming ingress)

### Overview
- **Azure Event Hubs**: Kafka‑compatible endpoints; storage/Data Lake datacasting to Kafka compatible endpoints.  
- **Amazon Kinesis Data Streams**: Shard or on‑demand capacity modes, scalable streaming. 
- **Google Pub/Sub**: Hard durable scalable pub/sub on large scale. 

### Monitoring & observability
- **Azure**: Event Hubs metrics/logs in the Azure Monitor.  
- **AWS**: Kinesis Streams CloudWatch metrics. 
- **GCP**: Pub/Sub Cloud Monitoring/Logging. 

### Pricing model (high‑level)
- **Event Hubs**: Pay for **throughput units** (Standard) or **capacity units** (Dedicated) + capture/storage.  
- **Kinesis Data Streams**: On‑demand capacity pay per shard hours/PUT payload units.  
- **Pub/Sub**: Storage by **bytes in/out** & network egress, Pay-per-byte.
 
### Strengths & weaknesses
- **Event Hubs**: + kafka‑compatibility makes migration easier; – handling TUs/CUs this takes some resource planning. 
- **Kinesis**: + Exact throughput control; − shard ability &occupation hot halve requirement ops concern.
- **Pub/Sub**: + rallies scaling/libs: - global and auto- scaling; - strict ordering/windowing might want to use Dataflow/Beam. 

---

### Examples (How to decide what to do)

- **Simple API or event processor** ->Functions / Lambda / Cloud Functions.  
- Long running process with retries and parallel branches -> Durable Functions / Step Functions / Workflows.  
- SaaS-to-SaaS automations with little code - Logic Apps / (Step Functions + AppFlow) / (Application Integration + Connectors).  
- Queueing and back-pressure between services -Service Bus / SQS / Pub-Sub (with pull subscribers).  
- Loosely coupled apps event bus** -> Event Grid / EventBridge / Eventarc.  
- **High- Throughput telemetry ingestion** Kinesis Streams / Pub/Sub / Event Hubs.

---



