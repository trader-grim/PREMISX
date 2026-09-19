# PREMIS(X) — Portable Role Environment Management Interface System

> **The Cryptographic Lock on the Enclosure Gate.**  
> PREMIS(X) is a POSIX-shaped, principal-agnostic capability standard designed to eliminate ambient authority hazards in autonomous AI agent runtimes.

---

## 📌 Overview

**PREMIS(X)** provides the core permission contract engine for **Catio OS**. Rather than granting AI agents direct, unmonitored access to system shells or broad API tools, PREMIS(X) enforces strict capability ceilings by evaluating every proposed task against signed execution contracts.

Identity in PREMIS(X) is principal-agnostic—human operators and AI agents execute under identical, declarative roles bounded by mathematical capability limits.

---

## ⚖️ The Core Security Invariants

PREMIS(X) guarantees four non-negotiable security bounds across the runtime:

1. **Roles Hold Permissions, Not Raw AIs:** AI models never hold ambient authority. Execution privileges reside strictly within versioned, cryptographically signed role contracts.
2. **Strict Provenance Baseline:** Agent roles cannot originate actions autonomously. Every execution path must root back to an explicit, signed human request.
3. **Bounded Transitive Invocation:** Discretionary scope expansion is hard-blocked. A role can only spawn sub-roles if explicitly authorized in the original task payload.
4. **The Capability Ceiling:** An agent's effective permission is strictly bounded by the invoking human's authority:

$$\text{Effective Permission} = \min(\text{Role Permissions}, \text{Requester's Permissions})$$

*An agent can never be used to launder privileges beyond what the invoking operator possesses.*

---

## 🔒 Runtime Execution Pipeline

```text
[ Signed Task Payload ]
           │
           ▼
┌───────────────────────────┐
│ PREMIS(X) Capability Gate │ ── Evaluates min(Role, Requester)
└─────────────┬─────────────┘
              │
              ▼
┌───────────────────────────┐
│ Algebraic Effect Classifier │ ── Maps intent to typed Choice/Noul tokens
└─────────────┬─────────────┘
              │
              ▼
┌───────────────────────────┐
│ eBPF LSM Kernel Maps      │ ── Drops unauthorized syscalls (EPERM) at hardware speed
└───────────────────────────┘
