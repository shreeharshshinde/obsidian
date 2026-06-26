Everybody has an intuitive idea of what it means for something to be reliable or unreliable. For software, typical expectations include:
• The application performs the function that the user expected.
• It can tolerate the user making mistakes or using the software in unexpected
ways.
• Its performance is good enough for the required use case, under the expected
load and data volume.
• The system prevents any unauthorized access and abuse.

> ***we can understand reliability as meaning, roughly, “continuing to work correctly, even when things go wrong.”***

> *The things that can go wrong are called faults, and systems that anticipate faults and can cope with them are called **fault-tolerant** or **resilient.*** 

Note that a **fault** is not the same as a **failure**. A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a
whole stops providing the required service to the user.

## Chaos Engineering & Deliberate Fault Injection

### Core Idea

In **distributed systems**, failures are **inevitable**, not exceptional.  
Instead of _hoping_ failures won’t happen, robust systems **intentionally trigger failures** to verify that fault-tolerance mechanisms actually work.

> **Untested fault tolerance is not fault tolerance — it is wishful thinking.**

---

### Why This Feels Counterintuitive

Intuition says:

> “Why break a system that is working?”

Reality:
- Most critical production bugs occur in **error-handling paths**
- Error paths are **rarely executed**
- Untested error paths **rot over time**

Therefore, systems often _appear_ fault tolerant but collapse during real failures.

---

## Faults vs Failures

- **Fault** → a component behaving incorrectly (crash, timeout, network drop)
- **Failure** → system unable to provide its service to users

Distributed systems commonly suffer from **partial failures**:
- One service fails
- Others continue running
- Assumptions break

---

## Chaos Engineering (Solution)

**Chaos Engineering** deliberately introduces faults into a system to:

- Continuously test fault-tolerance mechanisms
- Expose hidden assumptions
- Build confidence in system reliability

---

## Example: Chaos Monkey (built by Netflix)

Chaos Monkey:
- Randomly terminates production services
- Without warning
- During normal operation

Purpose:
- Validate auto-scaling
- Verify load balancer rerouting
- Test retry & timeout logic
- Ensure alerts trigger correctly

If killing a single node causes system failure → the system was never fault tolerant.

---

>***Although we generally prefer tolerating faults over preventing faults, there are cases where Prevention is better than Cure (e.g., because no cure exists).***

