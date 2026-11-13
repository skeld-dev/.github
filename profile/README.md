<picture>
  <source media="(max-width: 640px)" srcset="https://skeld-gh.devteam-203.workers.dev/header-mobile?v=1" />
  <img src="https://skeld-gh.devteam-203.workers.dev/header?v=1" width="1000" alt="Skeld. Your API. Under contract. A TypeScript backend framework for sensitive data." />
</picture>

Skeld makes limits, secret exposure and response checks part of how you define an API. Declare the contract separately from the handlers, then use that same contract in the client.

<picture>
  <source media="(max-width: 640px)" srcset="https://skeld-gh.devteam-203.workers.dev/contract-mobile?v=1" />
  <img src="https://skeld-gh.devteam-203.workers.dev/contract?v=1" width="1000" alt="One contract, both ends: declare bounds and classification; enforce schemas on the server; validate declared JSON responses in the client." />
</picture>

### The defaults are deliberate.

**Limits belong in the contract.** Strings, arrays and records require bounds. Leaving one unbounded takes an explicit reason.

**Secret exposure takes a decision.** A response schema containing a secret is rejected at startup unless its exposure is explicitly declared with a reason.

**The client checks, too.** Declared JSON responses are validated against the contract before the client returns typed data to your code.

---

Core is implemented. Authentication is next. The first public release is being prepared.

Created and maintained by [ul0gic](https://github.com/ul0gic).
