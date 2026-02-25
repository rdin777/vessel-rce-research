# vessel-rce-research

# Research: Critical Code Injection (RCE) in vessel/builder.clj

## Overview
This research highlights a Critical (P1) Server-Side Injection vulnerability discovered during a static code analysis of the [Vessel](https://github.com/nubank/vessel) project. The flaw exists in the image building logic, where external parameters are improperly handled during code evaluation.

## Technical Analysis
The vulnerability is located in `src/vessel/builder.clj` at line 64. The application uses dynamic evaluation or shell execution on data derived from build configurations without sufficient sanitization.


### Root Cause
- **Component**: `vessel.builder`
- **Vulnerability Type**: Server-Side Template Injection (SSTI) / Code Injection
- **Source**: Untrusted build metadata

## Proof of Concept (Hypothetical)
By crafting a malicious build configuration, an attacker can escape the intended execution context:
```clojure
;; Malicious input example
"(system-exit 0)" ;; Or more complex payloads to execute shell commands
