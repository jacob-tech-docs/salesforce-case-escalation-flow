# salesforce-case-escalation-flow
Shows an example use case with Flows and cases.

# Automating Case Escalation with Salesforce Flows

This guide walks through using Salesforce Flows to automate the escalation of high-priority cases that haven’t been updated within 2 business days.

## Table of Contents

- [Use Case](#use-case)
- [Why Use Flows?](#why-use-flows)
- [Steps](#steps)
  - [1️⃣ Create a New Flow](#1️⃣-create-a-new-flow)
  - [2️⃣ Configure the Trigger](#2️⃣-configure-the-trigger)
  - [3️⃣ Add a Scheduled Path](#3️⃣-add-a-scheduled-path)
  - [4️⃣ Add Get Records (Check Status)](#4️⃣-add-get-records-check-status)
  - [5️⃣ Add an Update Records Element](#5️⃣-add-an-update-records-element)
  - [6️⃣ Save and Activate](#6️⃣-save-and-activate)
- [Formula Snippet Example](#formula-snippet-example)
- [Conclusion and Next Steps](#conclusion-and-next-steps)

## Use Case

A company wants cases marked as "High" priority to escalate automatically if not updated within 2 business days.

## Why Use Flows?

Salesforce offers various tools for automating cases and other functionality. The best choice depends on the complexity of the use case. Salesforce recommends starting with declarative, no-code Flows and using Apex only when the use case is too complex for declarative tools.

## Steps

### 1️⃣ Create a New Flow

- Go to **Setup > Process Automation > Flows.**
- Click **New Flow.**
- Select **Record-Triggered Flow.**

---

### 2️⃣ Configure the Trigger

| Setting              | Value                                      |
|----------------------|--------------------------------------------|
| **Object**           | Case                                       |
| **Trigger**          | A record is created or updated             |
| **Entry Conditions** | Priority = "High"                          |
| **Optimization**     | Actions and Related Records                |

---

### 3️⃣ Add a Scheduled Path

- Add a **Scheduled Path:**
  - **Offset Number:** 2
  - **Offset Unit:** Days
  - **Time Source:** LastModifiedDate

---

### 4️⃣ Add Get Records (Check Status)

- Add **Get Records** to confirm the case is still open.
- Filter:
  - `Status != Closed`

---

### 5️⃣ Add an Update Records Element

- Update the Case’s **Escalated** field to `True`.

---

### 6️⃣ Save and Activate

- **Name:** Escalate High Priority Cases
- Save & Activate the Flow.

---

## Formula Snippet Example

**Priority Filter:**

```text
Priority = 'High'

AND(
    Priority = 'High',
    NOT(ISPICKVAL(Status, 'Closed'))
)
```
Conclusion and Next Steps
Congrats! You have successfully implemented a use case and are on your way to becoming a Salesforce professional. After developing this in a sandbox, update your Jira story or scrum board and have it tested by users in the sandbox. Once the users confirm the tests have passed, you are ready to deploy it to production using Change Sets or VS Code with the Salesforce CLI.
