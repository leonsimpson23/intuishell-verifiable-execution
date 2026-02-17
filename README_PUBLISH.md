# IntuiShell Proof Anchor  Demo (Sanitized)

This folder contains a reproducible PowerShell demo that illustrates a common operational gap:
the difference between **what systems log** and **what proves authority was asserted**.

**What this demo provides (safe to publish)**:
- public_key.xml  RSA public key you can use to verify sanitized proofs.
- PROOF/*.sanitized.json  proof artifacts (sanitized) that show payload_hash, signature, and public_key_fingerprint (no private key).
- logs/  internal logs that show the flow (for reviewers who run the demo locally).

**Important**: private_key.xml (local only) is gitignored automatically by the script. Do NOT publish it.

## Quick reading (Behavior  Assumption  Consequence  Question)
1. Behavior: Agent processes JSON instruction files and executes commands.
2. Assumption: The agent trusts the source/system that supplied the instruction.
3. Consequence: Logs show actions but do not cryptographically prove the instruction was authorized (replay/spoof risk).
4. Question (ownership trigger): Which team in your org would be accountable to prove an execution was authoritative and non-forged?

## How verification works (high-level)
- Signed instructions use RSA-SHA256 with a private key (kept locally).
- The gated agent verifies the signature using the **public_key.xml** and records a PROOF JSON with payload hash, signature, timestamp, and a public_key_fingerprint.
- The sanitized PROOF artifacts are safe to publish and verifiable by any reviewer using public_key.xml.

## To reproduce (local)
Run intuishell_proof_demo.ps1 on a Windows machine (PowerShell 5.1). It will:
- create sandbox files
- run a vulnerable agent example (shows attacker injection)
- run gated agent and record PROOF artifacts

