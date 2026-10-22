# Interview Preparation Roadmap guide

## 1. What the previous interview tells us

Based on the full interview conversation, this is not primarily an infrastructure engineering or coding interview.

The interviewers were much more interested in understanding whether the candidate could support critical banking applications, investigate production incidents, communicate with stakeholders, and take ownership of operational problems.

The discussion revealed several important details about the actual team.

Business-critical applications

The team supports CIBC and Simplii online/mobile banking, digital identity verification, fraud applications, live chat, AI services, and open banking.

Monitoring is more than checking errors

The team detects failed transactions, abnormal latency, traffic drops, and unusual business transaction patterns—even when applications report no errors.

Incident leadership and stakeholder management

The team coordinates multiple technical groups, leads postmortem reviews, manages conflicting opinions, and communicates with senior management.

24/7 operational responsibility

The team has onshore/offshore coverage, weekly on-call rotation, emergency changes, and after-hours production deployments.

### What the interviewer actually tested

The following weights are my suggested preparation priorities, not an official CIBC scoring rubric.

Incident management and problem management

30%

Monitoring, Dynatrace, Kibana and Splunk

25%

Communication, conflict and stakeholder management

20%

CI/CD, certificates and Azure fundamentals

15%

Banking reliability mindset and AI anomaly detection

10%

Key insight: A candidate who can explain the complete lifecycle of a banking production incident, including detection, communication, recovery, and prevention, will be better prepared for this interview than someone who only memorizes AWS or Kubernetes terminology.

## 2. Your five-day study schedule

Preparation tracker

0 of 5 completed

Day 1 — Core concepts and terminology

Thu, Oct 22 · 2 hours

Day 2 — Incident and problem management

Fri, Oct 23 · 3 hours

Day 3 — Monitoring and observability

Sat, Oct 24 · 3 hours

Day 4 — Communication and behavioral answers

Sun, Oct 25 · 2.5 hours

Day 5 — 40-minute mock interview

Mon, Oct 26 · 3 hours

Tuesday, October 27: final revision and a second practice round. Wednesday, October 28: 20–30 minutes of light review before the interview.

# Day 1 — Understand the role and its terminology

Thursday, October 22 | 2 hours

## Goal

Understand what an Application Reliability Engineer actually does, how the role differs from DevOps and SRE, and why banks require dedicated reliability teams.

### Step 1: Learn these 12 essential terms

| Term               | Beginner-friendly meaning                                                                                |
| ------------------ | -------------------------------------------------------------------------------------------------------- |
| Application        | Software that provides a service, such as mobile banking                                                 |
| Production         | The live environment used by real customers                                                              |
| DevOps             | Practices connecting development and operations to deliver software reliably                             |
| SRE                | Engineering practices focused on system reliability and automation                                       |
| ARE                | Application Reliability Engineering, focused on application health, incidents, and operational readiness |
| Tier 1 application | A business-critical application requiring the highest operational attention                              |
| Incident           | An unplanned interruption or degradation of service                                                      |
| P1 / P2            | Priority or severity categories, with P1 generally indicating a critical incident                        |
| On-call            | Being designated to respond to operational issues outside normal hours                                   |
| Runbook            | Documented steps for investigating or resolving known problems                                           |
| Escalation         | Engaging another team or senior specialist for assistance                                                |
| MTTR               | Mean Time to Restore/Recover, a measure of recovery speed                                                |

### Step 2: Understand a banking application's components

Simplified online banking transaction flow

Customer

Uses mobile or online banking

Frontend / API

Receives the request

Backend services and dependencies

Authentication

Transactions

External vendors

Response to customer

Transaction success, failure, or timeout

Conceptual illustration only; not CIBC's actual application architecture.

The key lesson is that an application can be running while a business transaction is failing. An ARE must monitor both technical health and customer outcomes.

### Step 3: Prepare these three interview answers

Q: What does Application Reliability Engineering mean to you?

> Application Reliability Engineering is about ensuring that critical applications remain available, perform well, and provide a reliable experience to customers. It involves proactive monitoring, responding to incidents, investigating root causes, and preventing recurring issues. The goal is not just to keep servers running, but to ensure important business transactions are working successfully.

Q: How is ARE different from DevOps?

> DevOps focuses heavily on improving software delivery, automation, and collaboration between development and operations. Application Reliability Engineering focuses more specifically on production application health, incident response, observability, and operational stability. The two overlap, especially in automation and deployment reliability.

Q: What does Tier 1 mean?

> A Tier 1 application is business-critical. If it becomes unavailable, it can significantly impact customers and business operations. That's why these applications need proactive monitoring, clear escalation procedures, and 24/7 support.

### Day 1 completion criteria

The candidate should be able to explain the role without notes, describe a simple online banking transaction, and explain why an application can fail even when its servers are healthy.

# Day 2 — Master incident and problem management

Friday, October 23 | 3 hours

This is the highest-priority study day because the interviewer spent considerable time discussing enterprise incident management, problem tickets, and postmortem leadership.

## Step 1: Memorize the incident lifecycle

Production incident response workflow

1

Detect

Monitoring alert or customer report

2

Assess impact

Which customers, services, and transactions?

3

Classify and escalate

Assign severity and engage the right teams

4

Investigate

Review metrics, logs, dependencies, and changes

5

Mitigate

Restore service safely

6

Validate recovery

Confirm customer transactions are successful

7

RCA and prevention

Document causes and track corrective actions

Memorize this sequence until it becomes automatic. It can answer several different interview questions.

## Step 2: Understand severity

| Severity      | Typical example                                           | Response                                         |
| ------------- | --------------------------------------------------------- | ------------------------------------------------ |
| P1 — Critical | Online banking unavailable to a large customer population | Immediate major incident coordination            |
| P2 — High     | Important transactions failing for a subset of customers  | Urgent investigation and escalation              |
| P3 — Medium   | Noncritical functionality degraded                        | Normal incident management with defined priority |
| P4 — Low      | Minor defect with limited impact                          | Scheduled resolution                             |

Actual severity definitions and escalation targets depend on the bank's internal policies.

## Step 3: Learn the difference between incident and problem management

Incident management: Restore service as quickly and safely as possible.

Problem management: Investigate the underlying causes and prevent future incidents.

Example: A banking API experiences repeated timeouts. The incident team restores service by rolling back a recent release. The problem management process later identifies an inefficient database query, tracks a permanent code fix, and adds monitoring to detect recurrence.

## Step 4: Understand postmortem leadership

The interviewers explicitly stated that their ARE team leads postmortem meetings.

The candidate must know how to structure one.

Suggested 30-minute postmortem agenda

| Time      | Discussion                              |
| --------- | --------------------------------------- |
| 0–5 min   | Incident summary and customer impact    |
| 5–10 min  | Incident timeline and detection         |
| 10–15 min | What went well and what did not         |
| 15–22 min | Root causes and contributing factors    |
| 22–27 min | Corrective and preventive actions       |
| 27–30 min | Action owners, deadlines, and follow-up |

Understand the difference between a root cause and a contributing factor. For example, an expired certificate might cause an outage, while missing expiry alerts and unclear certificate ownership are contributing factors that allowed it to happen.

### High-value interview answer

Q: One of our banking applications suddenly has a high failure rate. What would you do?

> First, I would acknowledge the alert and assess the business impact, including which customers and transactions are affected. I would check the monitoring dashboard to understand when the failure started and whether it's isolated to one service or affecting multiple applications.
>
> If it's a critical incident, I would escalate according to the severity process and engage the incident management team and relevant technical teams.
>
> During investigation, I would correlate application errors, logs, service dependencies, and recent deployments. My immediate priority would be restoring service safely, whether through a rollback or another approved mitigation.
>
> After recovery, I would verify that critical transactions are working and monitoring has returned to normal. Finally, I would participate in the RCA, identify preventive actions, and track them through completion.

### Day 2 practice

Rehearse the same scenario three times: once as a P1 outage, once as a partial transaction failure, and once as a recurring incident requiring a problem ticket.

# Day 3 — Monitoring, observability and reliability metrics

Saturday, October 24 | 3 hours

## Step 1: Understand monitoring versus observability

Monitoring tells you something is wrong.

Observability helps you understand what is wrong and why.

Learn the three pillars:

Metrics

What is happening?

Error rate, latency, traffic

Logs

What happened?

Errors, exceptions, events

Traces

Where did it happen?

Request journey across services

## Step 2: Understand the tools actually discussed

| Tool            | What to understand                                                                              |
| --------------- | ----------------------------------------------------------------------------------------------- |
| Dynatrace       | Application performance, response times, failure rates, dependency mapping, distributed tracing |
| Splunk          | Centralized logs, searching errors, investigating exceptions                                    |
| Kibana          | Viewing and searching logs stored in Elasticsearch                                              |
| Grafana         | Dashboards visualizing operational metrics                                                      |
| Azure Monitor   | Monitoring Azure resources and applications                                                     |
| GitHub Actions  | Automated software build, test, and deployment workflows                                        |
| Jenkins         | CI/CD pipeline automation                                                                       |
| Azure DevOps    | Software delivery and pipeline management                                                       |
| Azure Key Vault | Secure storage and management of secrets, keys, and certificates                                |
| NSG             | Azure network security rules controlling allowed traffic                                        |

The candidate should understand what each tool does and when to use it, without claiming hands-on experience they do not have.

## Step 3: Learn the four golden signals

Latency

How long requests take

Login takes 12 seconds

Traffic

How many requests arrive

Transfers drop from 1,000 to 100

Errors

How often requests fail

5% of payments fail

Saturation

How close a resource is to its limit

Database connection pool exhausted

## Step 4: Learn SLIs, SLOs, and SLAs

| Concept      | Simple explanation                   | Example                                                     |
| ------------ | ------------------------------------ | ----------------------------------------------------------- |
| SLI          | What we measure                      | Percentage of successful login requests                     |
| SLO          | What we aim to achieve               | 99.9% successful logins over 30 days                        |
| SLA          | Formal commitment                    | Contractual service availability commitment                 |
| Error budget | Permitted unreliability under an SLO | 0.1% of the measurement period for a 99.9% availability SLO |

For a 30-day, time-based availability SLO of 99.9%, the error budget is approximately 43.2 minutes.

## Step 5: Understand the most distinctive question from this interview

The interviewer described silent failures: transaction volumes may fall even when applications are not generating explicit errors.

Example: Transaction volume anomaly

Illustrative expected versus actual transactions per hour

Expected volumeActual volume

04008001.2K1.6K9 AM10 AM11 AM12 PM1 PM2 PM

Illustrative data, not actual bank metrics

The application may still return successful health checks, but the unexpected volume drop indicates a potential business transaction issue requiring investigation.

Q: How would you detect a transaction volume drop without errors?

> I would monitor business transaction volume in addition to technical error rates. I would compare current transaction volume against historical patterns for the same time of day and day of the week.
>
> If the volume drops unexpectedly, I would investigate whether customer traffic has changed, whether a downstream dependency is unavailable, or whether transactions are getting blocked before reaching the application.
>
> AI-based anomaly detection can help identify deviations from normal patterns without relying only on fixed thresholds. For low-volume applications, I would also monitor the expected time between successful transactions.

### Day 3 completion criteria

The candidate should be able to explain when to use Dynatrace versus Splunk, distinguish an SLI from an SLO, and describe why transaction volume monitoring is important in banking.

# Day 4 — Communication, conflict management and the SRE mindset

Sunday, October 25 | 2.5 hours

This is particularly important because the interviewers emphasized that the role involves speaking with senior managers, directors, application teams, and external stakeholders.

## Step 1: Learn how to communicate during a production incident

A good incident update should answer four questions:

1. What is happening?
2. What is the customer or business impact?
3. What actions are being taken?
4. When is the next update?

Example — speaking on a P1 incident bridge:

> We're currently investigating elevated transaction failures affecting the online banking service. The application and database teams are engaged, and we're reviewing recent changes and service dependencies to isolate the issue. Our immediate focus is restoring service and minimizing customer impact. We'll provide the next update in 15 minutes, or sooner if there's a significant development.

The 15-minute interval is illustrative; actual updates should follow the organization's incident communication policy.

## Step 2: Learn how to manage conflict

This was an explicit interview question.

Imagine that the application team says the problem is with the network, while the network team says the application is responsible.

A strong ARE does not immediately choose sides.

Use the FACT framework:

## F

Focus on impact

Remind everyone that restoring customer service is the priority.

## A

Assess evidence

Review logs, monitoring data, and the incident timeline.

## C

Clarify ownership

Assign parallel investigation tasks to the appropriate teams.

## T

Track decisions

Document findings, actions, and next steps.

Q: How would you handle conflict during an incident?

> During a production incident, different teams may have different opinions about the cause. My approach would be to remain calm, listen to each team's findings, and focus the discussion on technical evidence rather than assumptions.
>
> I would clarify which facts are confirmed, identify what still needs investigation, and assign clear next steps. If the disagreement delays recovery, I would involve the incident manager or appropriate technical lead.
>
> My priority would be restoring service, maintaining professional communication, and ensuring the incident review remains blameless.

## Step 3: Learn the STAR method

Use STAR for questions about past experience.

| Element   | What to explain                        | Suggested time |
| --------- | -------------------------------------- | -------------- |
| Situation | What problem existed?                  | 15 seconds     |
| Task      | What was your responsibility?          | 10 seconds     |
| Action    | What did you do?                       | 35 seconds     |
| Result    | What happened, and what did you learn? | 15 seconds     |

### Practice scenario: A production deployment fails

Use this as a hypothetical training example, not as a personal accomplishment unless the candidate has actually experienced it.

> We had a production deployment where the application started experiencing failures shortly after the release.
>
> My responsibility was to help investigate the issue and support service recovery.
>
> I would first review the deployment timeline and monitoring dashboards, then compare application logs before and after the release. If the evidence pointed to the deployment, I would coordinate with the application team to assess whether a rollback was the safest mitigation.
>
> After recovery, I would verify application health and successful business transactions. I would also recommend improving deployment validation and monitoring to reduce the risk of recurrence.

## Step 4: Learn how to handle unfamiliar technologies

A beginner must avoid presenting conceptual knowledge as production experience.

Q: Have you created Dynatrace dashboards?

> I understand how Dynatrace dashboards are used to monitor application response times, failure rates, throughput, and availability. I haven't independently built production Dynatrace dashboards yet, but I'm familiar with the monitoring concepts and would be comfortable learning the platform's dashboard configuration.

Q: Have you worked with Azure Key Vault?

> I understand that Azure Key Vault is used to securely manage application secrets, keys, and certificates. I haven't managed it extensively in production, but I understand its role in certificate lifecycle management and secure application configuration.

These answers are more credible than inventing experience, particularly when a senior engineer can ask detailed follow-up questions.

### Day 4 completion criteria

The candidate should be able to deliver a clear incident update, handle a disagreement professionally, and answer behavioral questions without rambling.

# Day 5 — Full 40-minute mock interview

Monday, October 26 | 3 hours

## Step 1: Rehearse the expected interview structure

The following is a suggested simulation based on the previous interview, not a confirmed agenda.

40-minute interview simulation

| 0–5 min   | Introduction and experience        |
| --------- | ---------------------------------- |
| 5–15 min  | Monitoring and troubleshooting     |
| 15–25 min | Incident and problem management    |
| 25–33 min | Technical fundamentals             |
| 33–37 min | Conflict and stakeholder scenarios |
| 37–40 min | Candidate questions and closing    |

## Step 2: Practice these 15 questions

These are based directly on the subjects raised by the interviewers.

Interactive mock interview

1 / 15

INTERVIEWER QUESTION

## Tell me about yourself and your background.

Show guidance

Next&#x20;

Answer aloud for 45–90 seconds before revealing the guidance. Record your answers to identify unclear explanations and unnecessary filler words.

## Step 3: Prepare an opening introduction

This is a template for a beginner. Replace the bracketed material with actual background and experience.

Thank you for the opportunity. My background is in [your actual education or professional experience], and I've been developing my understanding of application reliability, production support, and operational processes.

What interests me about Application Reliability Engineering is the combination of technical investigation, incident management, monitoring, and collaboration across teams.

I understand that supporting critical banking applications requires more than just checking whether servers are running. It's about monitoring customer transactions, identifying service degradation early, coordinating incident response, and preventing recurring issues.

I'm particularly interested in learning more about your team's use of Dynatrace, enterprise incident management, and AI-based anomaly detection. I believe my strengths in [your genuine strengths] would help me contribute while continuing to develop my technical expertise.

For an experienced candidate, this should be replaced with actual accomplishments and production experience.

## Step 4: Prepare a closing question

The previous interview revealed that the team has a steep learning curve and works with multiple lines of business.

A strong question would be:

> Given the number of critical applications your team supports, what would you expect someone joining this role to learn and take ownership of during their first three to six months?

This shows interest in operational responsibilities, learning expectations, and accountability.

# 3. Quick-reference technical cheat sheet

Review this before the interview.

## A. Troubleshooting frameworks

| Situation                     | Framework to remember                                              |
| ----------------------------- | ------------------------------------------------------------------ |
| High application failure rate | Impact → Logs → Dependencies → Mitigation → Validation             |
| Slow application              | Latency → Traffic → Resources → Database → Dependencies            |
| Pipeline failure              | Failed stage → Logs → Configuration → Credentials → Retry/validate |
| Certificate issue             | Expiry → Hostname → Chain → Binding → Renewal                      |
| Recurring incident            | Timeline → RCA → Contributing factors → Prevention                 |
| Stakeholder conflict          | Facts → Shared objective → Owners → Decision                       |
| Silent transaction failure    | Expected volume → Actual volume → Dependencies → Business impact   |

## B. Certificate management essentials

The interviewer specifically highlighted that the team manages many production certificates.

A beginner should understand:

- SSL/TLS certificate: Enables authenticated, encrypted connections, such as HTTPS.
- Certificate expiry: The certificate becomes invalid after its validity period.
- Certificate renewal: Obtaining or issuing a replacement certificate before expiry.
- Certificate chain: Links a server certificate to a trusted certificate authority.
- Certificate binding: Configuring the application, gateway, or load balancer to present the correct certificate.
- Azure Key Vault: Securely stores and manages certificates, keys, and secrets.

Practice answer:

> For certificate-related incidents, I would check the expiry date, hostname, certificate chain, and whether the correct certificate is configured on the application endpoint. If a certificate was recently renewed, I would also verify that the updated certificate is actually being presented to clients. For prevention, I would recommend centralized certificate inventory, clear ownership, and automated expiry alerts.

## C. CI/CD fundamentals

Typical CI/CD pipeline

Code

Build

Test

Scan

Deploy

A failed stage provides the starting point for troubleshooting.

Practice answer:

> I would first identify the exact pipeline stage that failed and review the execution logs. If it's a build issue, I'd investigate dependencies and configuration. If it's a deployment issue, I'd check credentials, permissions, target environment health, and deployment errors. After identifying the cause, I'd validate the fix and confirm that the pipeline completes successfully.

## D. High-impact terminology

These phrases are useful when the candidate understands their meaning.

| Phrase                                 | Appropriate context                   |
| -------------------------------------- | ------------------------------------- |
| Customer-impacting degradation         | Discussing service failures           |
| End-to-end transaction visibility      | Monitoring business processes         |
| Actionable alerts                      | Reducing monitoring noise             |
| Cross-functional incident coordination | Working with multiple teams           |
| Blameless postmortem                   | Incident reviews                      |
| Corrective and preventive actions      | Problem management                    |
| Mean Time to Restore (MTTR)            | Recovery performance                  |
| Business transaction monitoring        | Banking application health            |
| Baseline deviation / anomaly detection | AI-assisted monitoring                |
| Operational readiness                  | Preparing applications for production |
| Clear ownership and accountability     | Stakeholder management                |
| Continuous reliability improvement     | SRE mindset                           |

Avoid repeating these phrases mechanically. Use them only when they accurately describe the point being made.

# 4. Scenario practice: What would you do?

These five scenarios cover the most important reasoning patterns from the actual interview.

Scenario knowledge check

1 / 5

### Mobile banking logins suddenly fail for many customers.

Wait until more users complain

Assess impact, engage incident management, investigate authentication dependencies

Restart every server immediately

PreviousNext scenario&#x20;

# 5. Final revision: Tuesday and Wednesday

## Tuesday, October 27 — 90-minute consolidation

Use the day to reinforce what has already been studied rather than introduce many new topics.

15 min — Explain ARE, SRE, DevOps, and Tier 1 applications without notes

20 min — Rehearse a complete P1 incident lifecycle

15 min — Explain Dynatrace, Splunk, Kibana, and anomaly detection

15 min — Practice postmortem leadership and conflict management

15 min — Practice certificate and CI/CD troubleshooting

10 min — Rehearse introduction and closing question

## Wednesday, October 28 — Interview day

Review only the following:

- The seven-step incident lifecycle.
- Metrics, logs, and traces.
- The difference between incident and problem management.
- The silent transaction failure scenario.
- The conflict management framework.
- Your genuine experience examples and opening introduction.

Do not try to memorize entirely new technologies just before the interview.

# 6. What success looks like

A beginner does not need to become a production SRE in five days. The realistic goal is to understand the operational workflows well enough to discuss them accurately, respond to scenarios logically, and distinguish knowledge from practical experience.

Self-assessment scorecard

Practice readiness score

# 0/100

Self-rated, not a hiring prediction

Can explain ARE and Tier 1 banking support

Not ready

Basic

Good

Confident

Can describe incident response end to end

Not ready

Basic

Good

Confident

Understands monitoring tools and business metrics

Not ready

Basic

Good

Confident

Can explain postmortem and problem management

Not ready

Basic

Good

Confident

Can handle conflict and stakeholder communication

Not ready

Basic

Good

Confident

Can explain CI/CD and certificate fundamentals

Not ready

Basic

Good

Confident

Focus first on the incident lifecycle, monitoring fundamentals, and communication scenarios.

## The five principles to remember in the interview

Customer impact comes first. Application health is about successful banking transactions, not just healthy infrastructure.

Restore service before completing the RCA. Mitigate the incident safely, then investigate long-term prevention.

Monitoring must detect silent failures. A drop in transaction volume can be as important as an increase in errors.

Communication is part of reliability engineering. Coordinate teams, communicate impact, and keep stakeholders informed.

Every incident should produce learning. Postmortems, monitoring improvements, runbooks, and preventive actions help reduce recurrence.

Final recommendation: Spend roughly 60% of preparation time on incident management, monitoring, and stakeholder communication. Spend the remaining 40% on technical fundamentals, realistic examples, and interview delivery. That allocation most closely matches the emphasis of the interview conversation.

The candidate should aim to sound structured, calm, curious, and operationally aware, rather than pretending to have extensive production experience. A senior interviewer will often recognize the difference through follow-up questions.