# Danny B. Carr, Jr.

Security engineer working in PKI and certificate lifecycle automation, currently spending
most of my attention on post-quantum migration.

I publish measurements rather than opinions. Every claim in my work is labeled **Verified**
(measured here, with the script and captured output shipped alongside it), **Reported**
(cited to a standard or vendor document, not re-derived), or **Proposed** (designed, not
yet shipped or measured). The labels are dull on purpose.

## Measured corpora, archived and citable

Three repositories, each one a question nobody had published measurements for. Every cell
is a script plus its captured output, versions pinned per cell, and each carries a
`PRIOR-ART.md` recording what published work already covers. Those files have demoted my
own claims more than once, which is why they exist.

**[pqc-cert-matrix](https://github.com/DannyBCarrJr/pqc-cert-matrix)** ·
[10.5281/zenodo.21749600](https://doi.org/10.5281/zenodo.21749600)
What happens when a post-quantum or hybrid X.509 chain meets real client software. Eight
chain shapes against eleven client stacks, 88 cells.

- Parsing never fails. All 88 cells parse, so a parse-based certificate inventory has a
  100% false-pass rate on exactly the chains you care about.
- Windows splits against itself: CNG validates ML-DSA chains offline while schannel cannot
  complete a TLS handshake with them.
- Only rustls names the algorithm it rejected. Everyone else emits trust-store-shaped
  errors that send operators to the wrong layer.

**[pqc-chain-budget](https://github.com/DannyBCarrJr/pqc-chain-budget)** ·
[10.5281/zenodo.21846142](https://doi.org/10.5281/zenodo.21846142)
Post-quantum signature sizes projected onto each site's own deployed chain, on 8,152 real
chains captured from the Tranco top 10,000.

- Under a drop-in ML-DSA-44 migration, 85.1% of measured sites project past the IW10
  initial congestion window, an extra round trip per full handshake.
- Leaf-only migration fits almost everywhere: 0.3% exceed IW10.
- Certificate compression recovers a median 985 bytes today and roughly the same 985
  bytes after migration, which is 7.4% of an ML-DSA-44 chain. The saving is structural,
  and migration adds no structure.

**[pqc-chain-selection](https://github.com/DannyBCarrJr/pqc-chain-selection)** ·
[10.5281/zenodo.21911032](https://doi.org/10.5281/zenodo.21911032)
Which certificate chain a TLS 1.3 server actually sends when the client says which
signature algorithms it will accept. Five server stacks.

- Three of five sent a chain the client had said it would not accept, and every one of
  those handshakes completed.
- All three are conformant. RFC 8446 makes the constraint a SHOULD and tells a server
  with no acceptable chain to send one anyway, so a migration cannot rely on
  `signature_algorithms_cert` to keep a chain off the wire.
- rustls cannot honour it even if you want it to: the extension never reaches the
  certificate resolver.

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

## Writing

[carrdigital.dev/writing](https://carrdigital.dev/writing/), accuracy-first, every article
with a provenance section separating what I measured from what I am citing.

- [The typical chain moved](https://carrdigital.dev/writing/the-typical-chain-moved/)
- [The same 985 bytes](https://carrdigital.dev/writing/the-same-985-bytes/)
- [How much certificate can you afford?](https://carrdigital.dev/writing/how-much-certificate-can-you-afford/)
- [Hybrid certificates, weighed](https://carrdigital.dev/writing/hybrid-certificates-weighed/)
- [Expiry is the only revocation that works](https://carrdigital.dev/writing/expiry-is-the-only-revocation-that-works/)
- [The load-bearing word](https://carrdigital.dev/writing/the-load-bearing-word/)
- [What the AI actually broke (and what it didn't)](https://carrdigital.dev/writing/what-the-ai-actually-broke/)

## Tools

Three, all free, all backed by the corpora above rather than by estimates. Each one tells
you which of its numbers are measured and which are projected.

**[Handshake budget](https://carrdigital.dev/tools/handshake-budget/)** works out whether a
post-quantum certificate chain fits inside TCP's initial congestion window, and which
client stacks can actually complete the handshake.

**[Chain check](https://carrdigital.dev/tools/chain-check/)** looks up any top-10k domain,
shows its real certificate chain as measured, and checks whether that same chain still fits
the server's first flight once ML-DSA signs it. Per-site, from the measured data, with the
assumptions stated.

**[Certificate decoder](https://carrdigital.dev/tools/certificate-decoder/)** takes a
pasted X.509 certificate and shows its structure: tags, lengths, byte offsets, decoded
object identifiers, and key usage bits. It runs entirely in your browser and uploads
nothing, which for a tool that accepts certificates is the only defensible design.

## Etergis

[etergis.com](https://etergis.com), a digital continuity platform: encrypted storage with
delivery to the people who should receive it, on a schedule you control.

Zero-knowledge architecture, AES-256-GCM with AAD, Argon2id, X25519, and a versioned
envelope format so the cryptography can be upgraded without migrating anyone's data by
hand. The current envelope carries a hybrid X25519 and ML-KEM-768 key encapsulation for
the owner's at-rest copy, which is the surface that matters for harvest-now-decrypt-later.
Recipient delivery is an Argon2id passphrase wrap and is not hybrid, by decision, so I do
not describe the product as end-to-end post-quantum. FastAPI, Flutter, PostgreSQL,
Cloudflare, Render. Live on web, Google Play, and the App Store.

Architecture and whitepaper:
[Etergis-Docs](https://github.com/DannyBCarrJr/Etergis-Docs).

## Working with

`Python` `Dart/Flutter` `PowerShell` `Bash` `OpenSSL` `Docker` `PostgreSQL` `Cloudflare`
`GCP` `Wireshark`

CompTIA Security+, CySA+, CASP+. Currently working through Cloud+.

## Reaching me

Corrections are the most useful thing you can send. If a number in any of these
repositories disagrees when you rerun it, open an issue with the command that shows it and
I will fix it in the open.

For anything else: [carrdigital.dev](https://carrdigital.dev).
