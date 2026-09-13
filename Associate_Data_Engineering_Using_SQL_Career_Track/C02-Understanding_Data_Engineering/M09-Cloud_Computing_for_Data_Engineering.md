# Cloud Computing for Data Engineering

## Overview

**Cloud computing** allows companies to rent computing, storage, and database resources from cloud providers instead of owning and maintaining all physical infrastructure themselves.

Cloud computing is especially useful for data engineering because data processing workloads can vary significantly over time.

## On-Premises vs. Cloud Computing

### On-Premises

In an **on-premises** environment, a company owns and manages its own infrastructure.

This may require:

- Purchasing physical servers.
- Providing space for servers.
- Paying electricity costs.
- Maintaining hardware.
- Replacing and upgrading equipment.
- Moving servers when offices or data centers change.
- Provisioning enough capacity for peak processing workloads.

### Problem with On-Premises

Data processing workloads are not always continuous.

For example:

- Peak periods require high processing power.
- Quiet periods require much less processing power.

If infrastructure is sized for peak demand, some resources may remain unused during quieter periods.

This can lead to:

- Higher infrastructure costs.
- Underutilized resources.
- Higher maintenance costs.

## Cloud Computing

With cloud computing, companies **rent computing resources instead of purchasing and maintaining physical servers**.

Organizations can provision resources based on their needs and use them when required.

### Benefits

- Avoid purchasing physical servers.
- Avoid maintaining a dedicated server room.
- Scale resources according to demand.
- Pay for resources as they are used.
- Reduce infrastructure and maintenance costs.
- Avoid unused capacity during low-demand periods.
- Deploy resources in different geographical locations.
- Reduce latency by placing servers closer to users.

## Scalability

Cloud computing is useful when workloads vary over time.

Example:

**Low workload → Fewer resources**

**High workload → More resources**

This avoids having to permanently purchase enough hardware for the maximum possible workload.

## Geographic Distribution and Latency

The physical location of servers affects **latency**.

> **Closer server to the user → Lower network latency**

For companies serving customers globally, deploying resources in multiple geographical locations can improve application responsiveness.

## Cloud Computing for Data Storage

Cloud computing can also improve **database reliability and availability**.

A company needs to prepare for failures such as:

- Data center fires.
- Hardware failures.
- Natural disasters.
- Other infrastructure failures.

One way to improve resilience is to **replicate data in a different geographical location**.

### Geographic Replication

**Primary Location → Data Replication → Secondary Geographic Location**

If the primary location becomes unavailable, replicated data can help support continued operations.

## Cloud Security and Data Risks

Cloud computing also introduces risks.

If a company stores sensitive or confidential data with a cloud provider, it must consider:

- Data security.
- Privacy.
- Compliance requirements.
- Risks associated with third-party hosting.
- Government access or surveillance concerns.
- Security and governance across cloud environments.

> Cloud computing provides infrastructure benefits, but organizations remain responsible for properly managing security, governance, and compliance.

# Major Cloud Providers

The course identifies three major cloud providers:

1. **Amazon Web Services (AWS)**
2. **Microsoft Azure**
3. **Google Cloud**

## Common Cloud Services

| Category | AWS | Microsoft Azure | Google Cloud |
|---|---|---|---|
| **File/Object Storage** | Amazon S3 | Azure Blob Storage | Google Cloud Storage |
| **Compute** | Amazon EC2 | Azure Virtual Machines | Google Compute Engine |
| **Relational Database** | Amazon RDS | Azure SQL Database | Google Cloud SQL |

## Storage Services

### AWS

**Amazon S3**

Object/file storage service.

### Azure

**Azure Blob Storage**

Object storage service.

### Google Cloud

**Google Cloud Storage**

Object storage service.

## Compute Services

### AWS

**Amazon EC2**

Provides virtual computing resources.

### Azure

**Azure Virtual Machines**

Provides virtual machines for computation.

### Google Cloud

**Google Compute Engine**

Provides virtual machine-based computing.

## Database Services

### AWS

**Amazon RDS**

Managed relational database service.

### Azure

**Azure SQL Database**

Managed relational database service.

### Google Cloud

**Google Cloud SQL**

Managed relational database service.

# Spotflix Cloud Architecture

Spotflix chose **AWS**.

Its services are:

- **Amazon S3** → Stores album cover files.
- **Amazon EC2** → Processes songs.
- **Amazon RDS** → Stores employee information.

### Spotflix Example

**Album Covers → S3**

**Song Processing → EC2**

**Employee Database → RDS**

# Multicloud

**Multicloud** means using cloud services from **multiple cloud providers** instead of relying on only one provider.

An organization might use:

**AWS + Azure + Google Cloud**

## Advantages of Multicloud

### 1. Reduced Vendor Dependence

Using multiple providers reduces reliance on a single cloud vendor.

This can help reduce **vendor lock-in**.

### 2. Cost Optimization

Different providers may offer different prices or services.

Organizations can select services that provide better cost efficiency.

### 3. Legal and Regulatory Requirements

Some organizations may need to use particular infrastructure because of:

- Local laws.
- Regulatory requirements.
- Data residency requirements.

### 4. Disaster Resilience

Using multiple providers can provide additional redundancy.

If one cloud provider experiences an outage, workloads may be able to continue through another provider.

### Example

**Provider A outage → Workload can potentially fail over to Provider B**

This can reduce the impact of large-scale service disruptions.

## Multicloud Challenges

Multicloud also introduces additional complexity.

### 1. Vendor Lock-In

Cloud providers try to encourage customers to use more of their integrated services.

This can make migration to another provider difficult.

### 2. Compatibility

Services from different providers may not always be directly compatible.

For example:

**AWS Service A ↔ Azure Service B**

may require additional configuration or integration.

### 3. Security Complexity

Managing security across multiple cloud providers is more difficult.

Organizations must manage:

- Different security controls.
- Different identity systems.
- Different configurations.
- Different monitoring solutions.

### 4. Governance Complexity

Managing policies, compliance, and governance across multiple cloud environments is also more difficult.

# Cloud Computing Benefits vs. Risks

| Benefits | Risks / Challenges |
|---|---|
| Lower infrastructure costs | Security concerns |
| Pay for resources when needed | Privacy concerns |
| Scalable resources | Compliance requirements |
| Less physical infrastructure | Vendor lock-in |
| Geographic deployment | Cross-provider compatibility |
| Lower latency | More complex security management |
| Improved resilience | More complex governance |
| Reduced hardware maintenance | Dependence on cloud providers |

# Key Concepts

## On-Premises

**Company owns and manages infrastructure.**

## Cloud

**Company rents computing, storage, and other infrastructure from a provider.**

## Multicloud

**Company uses multiple cloud providers.**

## Vendor Lock-In

**Difficulty moving from one cloud provider to another because of provider-specific services, architectures, or dependencies.**

## Latency

**Delay experienced when data travels between a user and a server.**

Generally:

**Closer server → Lower latency**

## Geographic Redundancy

**Maintaining copies of data or infrastructure in different geographic locations to improve resilience.**

# Exam / Interview Key Points

- **Cloud computing** allows organizations to rent computing and storage resources rather than purchasing and maintaining all physical infrastructure themselves.
- On-premises infrastructure requires organizations to manage:
  - Servers
  - Physical facilities
  - Electricity
  - Hardware maintenance
  - Capacity planning
- Cloud computing helps avoid paying for unused processing capacity.
- Cloud resources can be provisioned according to current workload requirements.
- Cloud computing can help reduce infrastructure and maintenance costs.
- Deploying servers closer to users can reduce **latency**.
- Geographic replication improves resilience against data center failures and disasters.
- Sensitive or confidential data introduces additional **security, privacy, compliance, and governance considerations** when using cloud services.
- The three major cloud providers discussed are:
  - **AWS**
  - **Microsoft Azure**
  - **Google Cloud**
- AWS storage: **S3**
- Azure storage: **Blob Storage**
- Google Cloud storage: **Cloud Storage**
- AWS compute: **EC2**
- Azure compute: **Virtual Machines**
- Google Cloud compute: **Compute Engine**
- AWS relational database: **RDS**
- Azure relational database: **Azure SQL Database**
- Google Cloud relational database: **Cloud SQL**
- **Multicloud** means using multiple cloud providers.
- Multicloud can reduce vendor dependence and improve resilience.
- Multicloud can also increase:
  - Security complexity
  - Governance complexity
  - Integration complexity
  - Compatibility concerns
- Cloud providers may encourage **vendor lock-in** through integrated services.

# Quick Memory Aid

**AWS → S3 / EC2 / RDS**

- **S3** = Storage
- **EC2** = Compute
- **RDS** = Relational Database

**Azure → Blob / VM / SQL Database**

- **Blob** = Storage
- **Virtual Machines** = Compute
- **Azure SQL Database** = Database

**Google Cloud → Cloud Storage / Compute Engine / Cloud SQL**

- **Cloud Storage** = Storage
- **Compute Engine** = Compute
- **Cloud SQL** = Database

**Cloud = Rent resources**

**On-Premises = Own resources**

**Multicloud = Multiple cloud providers**

# Most Important Concept

> **Cloud computing allows organizations to access scalable computing, storage, and database resources without owning all the underlying physical infrastructure. It can reduce costs, improve scalability, geographic availability, and resilience, but introduces security, compliance, vendor lock-in, compatibility, and governance considerations.**
