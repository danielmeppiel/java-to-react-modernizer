---
name: Java to React Modernizer
description: Drive a verification-gated, security-reviewed migration of a Java application (Spring/JSP/Stripes/servlets) to React/JS via the java-to-react-modernizer skill
interval: manual
mode: interactive
model: claude-opus-4.6
input:
  - targets: "What to migrate: a Java source path, a module name, a set of classes/JSPs, or the literal word 'whole-app' to migrate the entire application. Optionally append the React target dir after '->' (e.g. 'src/main/webapp/account -> web/src/account')."
---

# Java to React Modernizer

Drive a staged, verification-gated migration of a Java application to
a React/JavaScript front end, using the **java-to-react-modernizer**
skill as the working spec. Activate the skill by name -- your harness
loads it from wherever skills live for you (this prompt is
harness-agnostic and makes no assumption about on-disk layout).

This is a banking-grade migration: build/test/lint/type verification
and a multi-lens security review are MANDATORY gates, and the final
write is human-approved.

Targets for this run: **${input:targets}**

## Procedure

1. ACTIVATE the **java-to-react-modernizer** skill. Treat its
   contents as authoritative for the phase contract (scope ->
   inventory+plan -> wave loop {migrate -> verify -> secure -> synth}
   -> human checkpoint -> final report) and for the operating
   invariants, the banking security invariants, the deterministic
   verification gates (`scripts/verify.sh`, `scripts/sast.sh`), the
   worker agents, and the receipt schemas. If the skill is not
   available in this harness, abort with a clear error naming it.

2. RESOLVE SCOPE from the targets input. If the input is 'whole-app',
   plan the full application; if it names a path/module/classes,
   migrate just that. If a React target dir was given after '->',
   use it; otherwise propose one and confirm at scope time.

3. EXECUTE the skill's workflow end to end. Do not skip the
   verification or security gates, and do not perform the
   irreversible system-of-record write (commit / open PR) without the
   human checkpoint approval the skill requires.

4. STOP at the human checkpoint and present the migration report plus
   the security attestation for approval before any write.

The skill is the single source of truth for HOW each phase runs --
this prompt only schedules and scopes the run.
