# Scheduling Data

## Overview

**Scheduling** is a key part of a data engineering system. It coordinates data processing tasks by determining **when tasks should run, in what order they should run, and how dependencies between tasks should be handled**.

> Scheduling is the **glue of a data engineering system**.

It can apply to many data processing tasks, including:

- Updating tables
- Updating databases
- Moving data
- Cleaning data
- Transforming data
- Validating data

## Why Scheduling Is Important

A data pipeline often contains many small tasks that depend on one another.

Scheduling helps:

- Run tasks in the correct order.
- Resolve task dependencies.
- Automate recurring tasks.
- Reduce unnecessary manual intervention.
- Coordinate different parts of a data pipeline.

### Example

**Task A → Task B → Task C**

If Task B depends on Task A, scheduling ensures that **Task A completes before Task B starts**.

# Scheduling Methods

There are three main approaches discussed in the lesson:

1. **Manual scheduling**
2. **Time-based scheduling**
3. **Sensor-based scheduling**

## 1. Manual Scheduling

A task is executed manually when someone requests it.

### Example

An employee moves from the **United States to Belgium**.

A person can manually update the employee database immediately.

### Advantages

- Simple for occasional tasks.
- Can execute immediately when requested.

### Disadvantages

- Depends on human intervention.
- More difficult to scale.
- Human errors can occur.
- Tasks may be forgotten or delayed.

> Data pipelines should generally be automated as much as practical.

## 2. Time-Based Scheduling

A task runs automatically at a specific time or according to a recurring schedule.

### Example

Update the employee database every morning at **6:00 AM**.

If a new employee was added the previous day, the change is reflected during the morning update.

### Common Uses

- Daily database updates
- Hourly processing
- Nightly financial processing
- Periodic data synchronization

### Example Schedule

**Every day at 6:00 AM → Update employees table**

## 3. Sensor Scheduling

**Sensor scheduling** runs a task when a specific condition is detected.

### Example

Update the departments table **only when a new employee is added** to the employees table.

This avoids running the task when there is nothing to update.

### Concept

**Condition detected → Trigger task**

### Advantage

- Avoids unnecessary processing.

### Disadvantage

- The sensor must continuously or regularly monitor for the condition.
- Monitoring requires additional resources.
- The extra resource cost may not always justify the benefit.

## Manual + Automated Scheduling

Manual and automated systems can work together.

### Example: Subscription Upgrade

A user manually upgrades their subscription in the Spotflix app.

The user's action triggers automated tasks that:

- Propagate the subscription change.
- Unlock new features.
- Update billing information.
- Update other relevant systems.

### Workflow

**User Action → Automated Pipeline Tasks → Updated Systems**

# Batch vs. Stream Processing

Another important consideration is **how data is ingested and processed**.

There are two main approaches discussed:

1. **Batch processing**
2. **Stream processing**

## Batch Processing

**Batch processing** means data is collected and processed in **groups at specific intervals**.

Instead of processing each record immediately, records accumulate and are processed together.

### Characteristics

- Data is processed in groups.
- Processing occurs at scheduled intervals.
- Often cheaper than continuous processing.
- Can be scheduled when resources are less busy.
- Commonly scheduled overnight or during off-peak periods.

### Spotflix Examples

- Songs uploaded by artists are sent to databases every **10 minutes**.
- Employee table updates occur every morning at **6:00 AM**.
- Revenue data for the finance department is updated overnight.

### Batch Example

**Records accumulate → Scheduled time → Process all records together**

## Stream Processing

**Stream processing** means individual data records are sent through the pipeline **as soon as they are updated or generated**.

### Characteristics

- Data is processed continuously.
- Records are handled individually or in a continuous flow.
- Provides faster availability of new data.
- Useful when users or systems need information immediately.

### Spotflix Example: New User

When a user signs up, their profile needs to be written to the database immediately so they can use the service.

Waiting 24 hours for the next batch would be unacceptable.

### Stream Example

**New Record → Immediately Sent Through Pipeline → Processed → Available**

# Batch vs. Stream

| Feature | Batch Processing | Stream Processing |
|---|---|---|
| **Data handling** | Groups of records | Individual/continuous records |
| **Timing** | Scheduled intervals | As data arrives |
| **Speed** | Delayed | Near-immediate |
| **Cost** | Often cheaper | Can require more continuous resources |
| **Best for** | Periodic updates | Immediate/continuous updates |
| **Example** | Daily employee update | User signup |

## Spotflix Batch Examples

- Songs processed every **10 minutes**.
- Employee updates processed every **6:00 AM**.
- Revenue table updated **overnight**.

## Spotflix Stream Examples

- New user signup.
- User profile updates that need immediate availability.
- Online music listening.

# Online vs. Offline Listening Example

The lesson also uses music listening to illustrate batch and stream processing.

### Online Listening

When a user listens online, Spotflix can stream parts of the song continuously.

**Song Parts → Stream One After Another → User**

This is similar to **stream processing**.

### Offline Listening

When a user saves a song for offline listening, all parts of the song need to be collected together so the complete file can be saved.

**Song Parts → Batch Together → Saved for Offline Use**

This illustrates **batch processing**.

# Real-Time Processing

There is also a third concept called **real-time processing**.

An example is:

- Fraud detection

In this course, **real-time and streaming are treated as essentially the same for simplicity**, because streaming is often associated with near-immediate processing.

> More precisely, real-time processing emphasizes strict timing requirements, while stream processing describes continuous data processing. They are related but are not inherently identical.

# Scheduling and Dependencies

Scheduling is especially important when tasks depend on one another.

Example:

**Ingest Data → Clean Data → Transform Data → Update Database → Generate Report**

The scheduler makes sure tasks happen in the correct sequence.

If the database cannot be updated until the data has been cleaned, then:

**Clean Data must complete before Update Database starts.**

# Scheduling Tools

Examples of data engineering scheduling tools include:

- **Apache Airflow**
- **Luigi**

These tools can help:

- Schedule tasks.
- Manage dependencies.
- Automate workflows.
- Monitor pipeline tasks.

# Key Differences

## Manual Scheduling

**Human triggers the task**

Example:

`Employee moves office → Person manually updates database`

## Time Scheduling

**Clock triggers the task**

Example:

`6:00 AM → Update employees table`

## Sensor Scheduling

**Condition triggers the task**

Example:

`New employee added → Update departments table`

## Batch Processing

**Process data in groups**

Example:

`Every 10 minutes → Process uploaded songs`

## Stream Processing

**Process data as it arrives**

Example:

`New user signup → Immediately update database`

# Exam / Interview Key Points

- **Scheduling is the glue of a data engineering system.**
- Scheduling coordinates tasks by controlling:
  - When tasks run.
  - The order in which tasks run.
  - Task dependencies.
- **Manual scheduling** requires human intervention.
- **Time-based scheduling** runs tasks at predetermined times or intervals.
- **Sensor scheduling** triggers tasks when a specific condition is detected.
- Sensor scheduling can reduce unnecessary processing but requires monitoring resources.
- Manual and automated processes can work together.
- **Batch processing** processes data in groups at scheduled intervals.
- Batch processing is often cheaper because it can be scheduled during periods of low resource usage.
- **Stream processing** processes individual data records as they are generated or updated.
- Stream processing is appropriate when data must become available quickly.
- Batch examples:
  - Songs every 10 minutes.
  - Employee updates at 6:00 AM.
  - Overnight revenue processing.
- Stream example:
  - Immediate processing of a new user signup.
- The lesson treats **real-time and stream processing as equivalent for simplification**, although the concepts are not strictly identical.
- **Apache Airflow** and **Luigi** are examples of scheduling tools.

# Quick Memory Aid

**Manual = Person**

**Time = Clock**

**Sensor = Condition**

**Batch = Groups**

**Stream = Continuous**

**Scheduling = Order + Time + Dependencies**

# Core Concept

> **Scheduling coordinates the tasks in a data engineering pipeline, while batch and stream processing determine how data is handled over time: batch processes data in groups at intervals, whereas stream processing handles data continuously as it arrives.**
