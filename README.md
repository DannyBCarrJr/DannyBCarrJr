# Danny B. Carr, Jr.

Security engineer working in PKI and certificate lifecycle automation, currently spending
most of my attention on post-quantum migration.

I publish measurements rather than opinions. Every claim in my work is labeled **Verified**
(measured here, with the script and captured output shipped alongside it), **Reported**
(cited to a standard or vendor document, not re-derived), or **Proposed** (designed, not
yet shipped or measured). The labels are dull on purpose.

## Post-Quantum, Measured

A practitioner's guide to moving real systems onto the NIST post-quantum standards
(FIPS 203, 204, 205): TLS, certificate hierarchies, and application crypto, with the lab
output shipped next to the claims.

- **[Leanpub](https://leanpub.com/post-quantum-measured)** (also on
  [Kindle](https://www.amazon.com/dp/B0HBW7VNSN))
- **[post-quantum-measured-lab](https://github.com/DannyBCarrJr/post-quantum-measured-lab)**
  is the runnable companion: every Verified number in the book, reproducible on stock
  OpenSSL on one laptop.
- Free whitepaper: [post-quantum-measured.pages.dev](https://post-quantum-measured.pages.dev)

## PQC certificate compatibility matrix

[**pqc-cert-matrix**](https://github.com/DannyBCarrJr/pqc-cert-matrix) answers a question
vendors were announcing products about without publishing measurements: when a
post-quantum or hybrid X.509 chain meets real client software, what actually happens?

Eight chain shapes against eleven client stacks, 88 cells, each one a script plus captured
output. Some of what it found:

- Parsing never fails. All 88 cells parse, so a parse-based certificate inventory has a
  100% false-pass rate on exactly the chains you care about.
- Windows splits against itself: CNG validates ML-DSA chains offline while schannel cannot
  complete a TLS handshake with them.
- Your runtime decides post-quantum readiness, not your distro.
- Only rustls names the algorithm it rejected. Everyone else emits trust-store-shaped
  errors that send operators to the wrong layer.

The repo also carries a `PRIOR-ART.md` recording what published work already covers, per
finding. It has demoted several of the project's own claims, which is the point of keeping
it.

## Writing

[carrdigital.dev/writing](https://carrdigital.dev/writing/), accuracy-first, every article
with a provenance section separating what I measured from what I am citing.

- [How much certificate can you afford?](https://carrdigital.dev/writing/how-much-certificate-can-you-afford/)
- [Hybrid certificates, weighed](https://carrdigital.dev/writing/hybrid-certificates-weighed/)
- [The load-bearing word](https://carrdigital.dev/writing/the-load-bearing-word/)
- [What the AI actually broke (and what it didn't)](https://carrdigital.dev/writing/what-the-ai-actually-broke/)

## Tools

**[Handshake budget calculator](https://carrdigital.dev/tools/handshake-budget/)**: work out
whether a post-quantum certificate chain fits inside TCP's initial congestion window, and
which client stacks can actually complete the handshake. Backed by the measured corpus
above rather than estimates, and it tells you which of its numbers are measured and which
are modelled.

## Etergis

[etergis.com](https://etergis.com), a digital continuity platform: encrypted storage with
delivery to the people who should receive it, on a schedule you control.

Zero-knowledge architecture, AES-256-GCM with AAD, Argon2id, X25519, Shamir secret
sharing, and a versioned envelope format so the cryptography can be upgraded without
migrating anyone's data by hand. The current envelope carries a hybrid X25519 and
ML-KEM-768 key encapsulation for the owner's at-rest copy. FastAPI, Flutter, PostgreSQL,
Cloudflare, Render. Live on web, Google Play, and the App Store.

Architecture and whitepaper:
[Etergis-Docs](https://github.com/DannyBCarrJr/Etergis-Docs).

## Working with

`Python` `Dart/Flutter` `PowerShell` `Bash` `OpenSSL` `Docker` `PostgreSQL` `Cloudflare`
`GCP` `Wireshark`

CompTIA Security+, CySA+, CASP+. Currently working through Cloud+.
