# governed-packs

Signed, governed harness packs for [Governed Studio](https://github.com/sskhangura82/governed-builder-harness).
Packs are distributed here **separately from the engine** — the honest real-world model: the platform
is one repo, the packs that plug into it are another.

Each release asset is a `.tar.gz` pack with a manifest carrying its **Ed25519 signature, signer
identity, signer tier, and pack hash**. You install a pack into your local Governed Studio and it lands
as a **CANDIDATE** — never active until a human promotes it. The marketplace is pull-and-review, not
install-and-trust.

## Verify locally — don't trust us

A pack you install is verified against **the publisher's public key that you pin out of band**, not a
key shipped inside the pack:

```bash
# install a pack from a release URL (unsigned/unknown-key packs land CANDIDATE-UNTRUSTED with a warning)
governed harness install <release-asset-url>
# pin the publisher's public identity you obtained independently, then re-verify → CANDIDATE
# promote by hand → ACTIVE (runs the meta-harness gate)
governed harness promote <harness_id>
```

First-party packs published here are signed by the Governed Studio release authority
(`release_authority` tier). Its public-key fingerprint is published out of band in the engine repo
(`docs/release_authority_public_identity.json`). Pin that; verify against it.

## What Governed Studio does — and does not

Governed Studio does **not**:
- prove that software is universally safe
- guarantee compliance with FDA, IEC 62304, the EU AI Act, HIPAA, or any regulatory framework
- replace physician judgment or clinical expertise
- provide medical advice
- certify AI products for clinical deployment

Governed Studio **does**:
- produce cryptographically signed evidence that named artifacts satisfied named claims under named authority
- generate auditable, evidence-backed governance artifacts aligned with emerging standards
- enable falsification-first behavioral verification before deployment
- maintain an immutable evidence trail from build through verification to sign-off

## Labeling

Any pack demonstrating a clinical workflow ships as a **synthetic demonstration on synthetic data — NOT
for clinical use, NOT FDA-cleared, NOT medical advice**. Packs published here carry their own labeling;
read each pack's README before use.

## No telemetry

Governed Studio does not collect telemetry, usage analytics, crash reports, or any data from your
machine. There is no code path that transmits your data. Your evidence stays on your machine. The only
outbound calls it ever makes are ones you explicitly configure (an installed pack fetch you initiate, or
a webhook URL you register).
