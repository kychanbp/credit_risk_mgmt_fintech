# The State of Loans: Modeling Loan Core as a Finite State Machine

**Bridging computer science and credit systems through the language of states and transitions**

Loan management systems — or *loan core* — form the backbone of financial institutions. They govern the business logic behind loan creation, approval, disbursement, and repayment — in short, the entire loan cycle.

In abstract form, a loan core defines the *states* of a loan, the *actions* that can be taken (by users or by the system through auto-triggers), and the *transitions* between these states. When I began learning more about computational theory, it struck me that a loan core is, at its essence, a **state machine**.

It has to be — because a computer itself is a state machine. Viewing loan core through the lens of computational theory not only gives a formal framework for understanding how it works, but also helps navigate the various implementations across institutions. Beneath all the different designs and data structures, the logic can be abstracted into one thing: a finite state machine.

---

## A Simplified Loan Core Example

Consider a minimal version of a loan core system.

A new loan starts in an initial state and moves through a sequence of states based on user actions or automated events:

```
[start] → (create) → [Pending] → (approve) → [Approved] → (disburse) → [Active] → (full repayment) → [Closed]
                                       ↘ (reject)
                                           [Rejected]
```

Each arrow represents a *transition* triggered by an event such as "approve" or "disburse." The machine ensures that only valid transitions occur — for example, a loan can't be disbursed before it's approved.

A **finite state machine (FSM)** is, by definition, a machine that — at any given moment — is in a single state. When it receives an input, it looks up its transition table to determine the next state, and possibly what output or action to produce.

---

## Formal Definition

Formally, a finite state machine can be defined as a five-tuple:

$$
M = (Q, \Sigma, \delta, q_0, F)
$$

where:

- **Q** is the finite set of states.
- **Σ** is the finite set of possible inputs (the *alphabet*).
- **δ** is the transition function: $Q \times \Sigma \to Q$.
- **q₀** ∈ **Q** is the start state.
- **F** ⊆ **Q** is the set of accept (or terminal) states.

Applied to our toy loan core:

- **Q = { null, pending, approved, rejected, active, closed }**
- **Σ = { create, approve, reject, disburse, full_repayment }**
- **q₀ = null**
- **F = { rejected, closed }**

---

## Transition Table

| Current State | create   | approve  | reject   | disburse | full repayment |
|---------------|----------|----------|----------|----------|----------------|
| start         | pending  | start    | —        | —        | —              |
| pending       | —        | approved | rejected | —        | —              |
| approved      | —        | approved | —        | active   | —              |
| rejected      | —        | rejected | —        | —        | —              |
| active        | —        | —        | —        | —        | closed         |
| closed        | —        | —        | —        | —        | closed         |

This simple table captures the essence of loan lifecycle logic — an ordered system of possible transitions bounded by rules.

Real-world loan cores, however, are not purely finite state machines. They are **Extended Finite State Machines (EFSMs)**, which means transitions can depend on external conditions (e.g., whether the account has sufficient balance, or whether the disbursement date has arrived). EFSMs include *guards* and *context variables* to control when a transition is valid, making them far more expressive than classical FSMs.

---

## From Theory to Reality: Apache Fineract

One open-source example that demonstrates this beautifully is **Apache Fineract**, a microfinance and loan management platform.

Fineract implements an extended state machine for loan lifecycle management. Each state (like *Approved*, *Active*, or *Overpaid*) can respond to a wide range of *events* — such as disbursal, repayment, write-off, or reschedule.

The following **state transition matrix** illustrates how complex this system becomes once we consider real-world business rules.

---

### State Transition Matrix

#### Complete δ(Q, Σ) Matrix

This matrix shows **all possible (state, event)** combinations. Each cell contains the resulting state or an indicator of how the system handles that input.

**Legend:**
- ✓ = Valid transition (always allowed)
- C = Conditional transition (depends on context)
- \- = Invalid/blocked transition
- A = Auto-transition (system-triggered)

**Event Abbreviations:**

| Code | Event                    | Code | Event                    |
|------|--------------------------|------|--------------------------|
| CR   | CREATED                  | WO   | WRITE_OFF                |
| RJ   | REJECTED                 | WU   | WRITE_OFF_UNDO           |
| AP   | APPROVED                 | RS   | RESCHEDULE               |
| WD   | WITHDRAWN                | OV   | OVERPAYMENT              |
| DB   | DISBURSED                | CA   | CHARGE_ADDED             |
| AU   | APPROVAL_UNDO            | CX   | CHARGE_ADJUSTMENT        |
| DU   | DISBURSAL_UNDO           | CB   | CHARGEBACK               |
| CP   | CHARGE_PAYMENT           | AT   | ADJUST_TRANSACTION       |
| RW   | REPAYMENT_OR_WAIVER      | IT   | INITIATE_TRANSFER        |
| RF   | REPAID_IN_FULL           | RT   | REJECT_TRANSFER          |
|      |                          | WT   | WITHDRAW_TRANSFER        |
|      |                          | CR   | CREDIT_BALANCE_REFUND    |

#### Main Transition Matrix

```
Current State             │ CR│ RJ│ AP│ WD│ DB│ AU│ DU│ CP│ RW│ RF│ WO│ WU│ RS│ OV│ CA│ CX│ CB│ AT│ IT│ RT│ WT│ CR│
──────────────────────────┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
null                      │ ✓ │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │
SUBMITTED_PENDING_APPROVAL│ - │ ✓ │ ✓ │ ✓ │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │
APPROVED                  │ - │ - │ - │ - │ ✓ │ ✓ │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │
ACTIVE                    │ - │ - │ - │ - │ - │ - │ ✓ │ - │ - │ A │ ✓ │ - │ ✓ │ A │ - │ - │ - │ - │ ✓ │ - │ - │ - │
TRANSFER_IN_PROGRESS      │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ ✓ │ ✓ │ - │
TRANSFER_ON_HOLD          │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │
WITHDRAWN_BY_CLIENT       │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │
REJECTED                  │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │
CLOSED_OBLIGATIONS_MET    │ - │ - │ - │ - │ C │ - │ - │ C │ C │ - │ - │ - │ - │ A │ ✓ │ ✓ │ ✓ │ C │ - │ - │ - │ - │
CLOSED_WRITTEN_OFF        │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ ✓ │ - │ - │ - │ - │ - │ C │ - │ - │ - │ - │
CLOSED_RESCHEDULE_AMOUNT  │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ - │ C │ - │ - │ - │ - │
OVERPAID                  │ - │ - │ - │ - │ - │ - │ - │ C │ C │ ✓ │ - │ - │ - │ - │ - │ - │ ✓ │ - │ - │ - │ - │ A │
```

---

## Why Model Loan Core as a (Extended) Finite State Machine?

### 1. Clarity by construction

- **Single source of truth:** Every legal state and transition is explicit. No "mystery paths."
- **Domain glossary:** States become shared nouns (*Approved, Active, Overpaid*). Events become verbs (*Disburse, Write-off*).
- **Invariants surface naturally:** e.g., "You can't *Disburse* unless `state=Approved`."

### 2. Safer change management

- Adding or modifying a rule means changing a row or column, not sprinkling conditions across services.
- Impact radius is clear — a diff in the matrix shows exactly what changed.

### 3. Testability and automation

- Every `(state, event)` combination forms a test case.
- Guards can be expressed as preconditions, making policy validation deterministic.
- Simulations and replays become trivial.

### 4. Compliance and auditability

- "Why is this loan *Closed*?" — replay the event history through the transition function δ.
- Policies become readable tables, not hidden logic.
- Invalid paths are blocked by design.

### 5. Operational resilience

- Side effects attach to transitions, making idempotency and retries safe.
- State recovery after failure is simple: restore the last `(state, context)` pair.

### 6. Product velocity without chaos

- New product features become guarded transitions, not rewrites.
- Variant testing (FSM v1 vs v2) is safe and measurable.

---

## Seeing Systems as State Machines

Modeling a system as a state machine is not just an academic exercise — it's a way of *thinking*. It forces every assumption about what can happen, when, and under what conditions to become explicit. The loan core stops being a black box of code and business rules, and turns into a living map of states and transitions. You can reason about it, test it, simulate it, and explain it. Most importantly, it gives teams a shared grammar for complexity — engineers, risk analysts, and operations staff can finally point to the same table and agree on what "Active" or "Closed" really means.

---

## Beyond the State Machine

The state machine captures the *skeleton* of the loan core — the structure of states and valid transitions. But the living body of the system includes many other organs working in sync.

At the heart of it are **transaction functions** that handle money movement: *disbursement*, *repayment*, *fees*, and *penalties*. Each of these operations changes not only account balances but also the loan's internal context — triggering new transitions in the state machine.

Surrounding this are **repayment schedule generators**, which determine expected installments and interest accruals; and **fee and penalty managers**, which apply business rules dynamically over time. Beyond the core logic, other crucial layers complete the ecosystem:

- **Account management**, which maintains borrower and product relationships.
- **Accounting**, which records journal entries and enforces financial integrity.
- **API and service layers**, which expose the system's functions to external modules like mobile apps or credit platforms.

Thinking in FSM terms doesn't replace these subsystems — it organizes them. The state machine becomes the *control plane* that orchestrates when and how these modules act. By defining the legal transitions clearly, every financial operation — from posting a repayment to writing off a loan — has a well-defined place in the broader choreography.

---

## Further Reading

- **Michael Sipser**, *[Introduction to the Theory of Computation (Third Edition)](https://www.cengage.com/c/introduction-to-the-theory-of-computation-3e-sipser/9781133187790/)* — a formal yet intuitive foundation for finite automata, regular languages, and computational limits.
- **Robert Nystrom**, *[Game Programming Patterns – The State Pattern](https://gameprogrammingpatterns.com/state.html)* — a practical, accessible introduction to state machines in real software systems.
