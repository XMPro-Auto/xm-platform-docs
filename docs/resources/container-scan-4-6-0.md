---
title: Container Security Scan Report - XMPro 4.6.0
description: Trivy container vulnerability scan results for XMPro 4.6.0 images, including per-image findings and false positive analysis.
---

## Container Security Scan Report - XMPro 4.6.0

**Registry:** xmpro.azurecr.io
**Version:** 4.6.0
**Scan Date:** March 17, 2026
**Scanner:** Trivy v0.61.0
**Vulnerability Database:** 2026-03-17

## Executive Summary

Security vulnerability scan of all XMPro 4.6.0 container images from `xmpro.azurecr.io`, including three Stream Host variants (bookworm-slim, bookworm-slim-python3.12, alpine3.21).

All **Critical** and **High** severity findings have been investigated and confirmed as **false positives**. Investigation and mitigation of the remaining Medium and Low severity findings did not make the 4.6.0 release schedule. These will be reviewed and addressed in upcoming releases as part of our ongoing security improvement process.

> [!NOTE]
> The totals below cover the four core product images: ad, ds, ai, and stream-host (bookworm-slim default). The [per-image overview](#per-image-overview) below shows counts for all six image variants individually.

| Severity | Count |
|----------|-------|
| Critical | 1 |
| High | 3 |
| Medium | 36 |
| Low | 113 |
| **Total** | **153** |

## Per-Image Overview

> [!NOTE]
> Counts are per image variant. CVEs that appear in multiple images (e.g. a system library vulnerability present in both bookworm-slim and bookworm-slim-python3.12) are counted separately in each row.

| Image | Critical | High | Medium | Low | Total |
|-------|----------|------|--------|-----|-------|
| **ad** - App Designer | 0 | 0 | 2 | 0 | **2** |
| **ds** - Data Stream Designer | 0 | 0 | 2 | 0 | **2** |
| **ai** - AI | 0 | 0 | 7 | 2 | **9** |
| **stream-host** - bookworm-slim (default) | 1 | 3 | 25 | 111 | **140** |
| **stream-host** - bookworm-slim-python3.12 | 2 | 3 | 28 | 116 | **149** |
| **stream-host** - alpine3.21 | 0 | 0 | 0 | 0 | **0** |

## Image Details

### ad - App Designer

`xmpro.azurecr.io/ad:4.6.0`

**Scan result:** 0 Critical, 0 High, 2 Medium, 0 Low

**Medium severity (2):**

- **MimeKit:** CVE-2026-30227 (2 instances)

---

### ds - Data Stream Designer

`xmpro.azurecr.io/ds:4.6.0`

**Scan result:** 0 Critical, 0 High, 2 Medium, 0 Low

**Medium severity (2):**

- **MimeKit:** CVE-2026-30227 (2 instances)

---

### ai - AI

`xmpro.azurecr.io/ai:4.6.0`

**Scan result:** 0 Critical, 0 High, 7 Medium, 2 Low

**Medium severity (7):**

- **Azure.Identity:** CVE-2024-29992, CVE-2024-35255
- **Microsoft.Identity.Client:** CVE-2024-35255
- **System.Security.Cryptography.Xml:** CVE-2022-34716

**Low severity (2):** Low and negligible severity vulnerabilities in system libraries.

---

### stream-host - bookworm-slim (default)

`xmpro.azurecr.io/stream-host:4.6.0`

**Scan result:** 1 Critical, 3 High, 25 Medium, 111 Low

#### Critical Severity (1) - Confirmed False Positive

| CVE ID | Package | Status |
|--------|---------|--------|
| CVE-2023-45853 | zlib1g (1:1.2.13.dfsg-1) | **FALSE POSITIVE** - zlib integer overflow in MiniZip contrib. XMPro uses .NET System.IO.Compression, not MiniZip. |

#### High Severity (3) - All Confirmed False Positives

| CVE ID | Package | Status |
|--------|---------|--------|
| CVE-2026-0861 | libc-bin (2.36-9+deb12u13) | **FALSE POSITIVE** - glibc size/alignment params not reachable in container. |
| CVE-2026-0861 | libc6 (2.36-9+deb12u13) | **FALSE POSITIVE** - glibc size/alignment params not reachable in container. |
| CVE-2023-2953 | libldap-2.5-0 (2.5.13+dfsg-5) | **FALSE POSITIVE** - libldap null pointer deref. Library installed but unused. |

#### Medium Severity (25)

Key affected packages:

- **curl / libcurl4:** CVE-2026-1965, CVE-2026-3783 and others. *curl is installed but .NET HttpClient is used instead.*
- **gpgv:** CVE-2025-30258, CVE-2025-68972. *gpgv not used by application.*
- **libc-bin / libc6:** CVE-2025-15281, CVE-2026-0915. *wordexp/getnetbyaddr not called by application.*
- **libpam-modules / libpam-modules-bin / libpam-runtime / libpam0g:** CVE-2024-10041
- **libsystemd0:** CVE-2026-4105

> [!NOTE]
> **False positive summary:** 1 Critical + 3 High + 8 Medium CVEs are confirmed false positives. Remaining real findings: 0 Critical, 0 High, 17 Medium.

#### Low Severity (111)

Low and negligible severity vulnerabilities in system libraries and packages.

---

### stream-host - bookworm-slim-python3.12

`xmpro.azurecr.io/stream-host:4.6.0-bookworm-slim-python3.12`

**Scan result:** 2 Critical, 3 High, 28 Medium, 116 Low

#### Critical Severity (2) - All Confirmed False Positives

| CVE ID | Package | Status |
|--------|---------|--------|
| CVE-2025-7458 | libsqlite3-0 (3.40.1-2+deb12u2) | **FALSE POSITIVE** - SQLite integer overflow. Python variant dependency, not used by .NET app. |
| CVE-2023-45853 | zlib1g (1:1.2.13.dfsg-1) | **FALSE POSITIVE** - zlib integer overflow in MiniZip contrib. XMPro uses .NET System.IO.Compression, not MiniZip. |

#### High Severity (3) - All Confirmed False Positives

| CVE ID | Package | Status |
|--------|---------|--------|
| CVE-2026-0861 | libc-bin (2.36-9+deb12u13) | **FALSE POSITIVE** - glibc size/alignment params not reachable in container. |
| CVE-2026-0861 | libc6 (2.36-9+deb12u13) | **FALSE POSITIVE** - glibc size/alignment params not reachable in container. |
| CVE-2023-2953 | libldap-2.5-0 (2.5.13+dfsg-5) | **FALSE POSITIVE** - libldap null pointer deref. Library installed but unused. |

#### Medium Severity (28)

Key affected packages:

- **curl / libcurl4:** CVE-2026-1965, CVE-2026-3783 and others. *curl is installed but .NET HttpClient is used instead.*
- **gpgv:** CVE-2025-30258, CVE-2025-68972. *gpgv not used by application.*
- **libc-bin / libc6:** CVE-2025-15281, CVE-2026-0915. *wordexp/getnetbyaddr not called by application.*
- **libncursesw6:** CVE-2023-50495
- **libpam-modules / libpam-modules-bin / libpam-runtime / libpam0g:** CVE-2024-10041

> [!NOTE]
> **False positive summary:** 2 Critical + 3 High + 8 Medium CVEs are confirmed false positives. Remaining real findings: 0 Critical, 0 High, 20 Medium.

#### Low Severity (116)

Low and negligible severity vulnerabilities in system libraries and packages.

---

### stream-host - alpine3.21

`xmpro.azurecr.io/stream-host:4.6.0-alpine3.21`

**Scan result:** 0 Critical, 0 High, 0 Medium, 0 Low

> [!TIP]
> No vulnerabilities detected. This image has the smallest attack surface of all Stream Host variants.

## False Positive Assessments

Related: [v4.6.0 Release Notes](../release-notes/index.md#v460)

The following CVEs were assessed as false positives. The affected components are either not present in XMPro deployments or are not reachable in the container runtime environment.

- [CVE-2005-2541](https://www.cve.org/CVERecord?id=CVE-2005-2541): GNU tar setuid extraction is intended POSIX behavior; Debian and Red Hat classify as "won't fix".
- [CVE-2010-4756](https://www.cve.org/CVERecord?id=CVE-2010-4756): glibc glob() resource consumption is POSIX-specified behavior; won't fix.
- [CVE-2015-3276](https://www.cve.org/CVERecord?id=CVE-2015-3276): openldap TLS cipher acceptance issue; XMPro uses .NET LDAP, not libldap directly.
- [CVE-2016-2781](https://www.cve.org/CVERecord?id=CVE-2016-2781): coreutils chroot TIOCSTI escape; kernel mitigated since Linux 6.4.4.
- [CVE-2017-17740](https://www.cve.org/CVERecord?id=CVE-2017-17740): openldap contrib/slapd-modules DoS; Debian doesn't build contrib modules.
- [CVE-2017-18018](https://www.cve.org/CVERecord?id=CVE-2017-18018): coreutils chown race condition; kernel hardening (fs.protected_regular) mitigates.
- [CVE-2018-5709](https://www.cve.org/CVERecord?id=CVE-2018-5709): krb5 integer overflow in policy lifetime; trusted admin input only.
- [CVE-2018-6829](https://www.cve.org/CVERecord?id=CVE-2018-6829): libgcrypt20 ElGamal side-channel; XMPro uses OpenSSL, hybrid mode unaffected.
- [CVE-2018-20225](https://www.cve.org/CVERecord?id=CVE-2018-20225): pip vulnerable --extra-index-url option is never used in XMPro Stream Host.
- [CVE-2018-20796](https://www.cve.org/CVERecord?id=CVE-2018-20796): glibc regex recursion DoS; disputed, glibc maintainers don't consider this a security issue.
- [CVE-2019-1010022](https://www.cve.org/CVERecord?id=CVE-2019-1010022): libc-bin (glibc) disputed CVE; glibc upstream states "not a real threat", requires prior stack overflow.
- [CVE-2019-1010023](https://www.cve.org/CVERecord?id=CVE-2019-1010023): glibc ldd requires user to run on malicious ELF; documented behavior.
- [CVE-2019-1010024](https://www.cve.org/CVERecord?id=CVE-2019-1010024): glibc ASLR bypass via exception messages; kernel security feature, not glibc bug.
- [CVE-2019-9192](https://www.cve.org/CVERecord?id=CVE-2019-9192): glibc regex recursion DoS; same issue as CVE-2018-20796.
- [CVE-2022-0563](https://www.cve.org/CVERecord?id=CVE-2022-0563): util-linux chfn/chsh readline echo; Debian uses shadow package instead.
- [CVE-2022-27943](https://www.cve.org/CVERecord?id=CVE-2022-27943): gcc libiberty Rust demangling in dev tools only; negligible impact.
- [CVE-2023-2953](https://www.cve.org/CVERecord?id=CVE-2023-2953): libldap-2.5-0 null pointer dereference; no LDAP functionality used in Stream Host containers.
- [CVE-2023-31486](https://www.cve.org/CVERecord?id=CVE-2023-31486): perl HTTP::Tiny TLS verification issue; XMPro uses .NET HttpClient, not Perl.
- [CVE-2023-42465](https://www.cve.org/CVERecord?id=CVE-2023-42465): sudo ROWHAMMER hardware attack; impractical in cloud environments with ECC RAM.
- [CVE-2023-45853](https://www.cve.org/CVERecord?id=CVE-2023-45853): zlib integer overflow in MiniZip contrib; XMPro uses .NET System.IO.Compression, not MiniZip.
- [CVE-2024-1013](https://www.cve.org/CVERecord?id=CVE-2024-1013): Alpine unixodbc example code only, not compiled in XMPro containers.
- [CVE-2025-6020](https://www.cve.org/CVERecord?id=CVE-2025-6020): libpam requires pam_namespace polyinstantiation, not used in XMPro containers.
- [CVE-2025-6297](https://www.cve.org/CVERecord?id=CVE-2025-6297): dpkg only affects manual dpkg-deb extraction, not used in XMPro containers.
- [CVE-2025-7458](https://www.cve.org/CVERecord?id=CVE-2025-7458): libsqlite3-0 Python variant only; requires crafted SQL with large ORDER BY, not possible in XMPro containers.
- [CVE-2025-9086](https://www.cve.org/CVERecord?id=CVE-2025-9086): curl is installed but not invoked at runtime; Stream Host runs as non-root app user with no curl usage in entrypoint or application code.
- [CVE-2025-9708](https://www.cve.org/CVERecord?id=CVE-2025-9708): KubernetesClient 4.0.26 is a transitive dependency of AspNetCore.HealthChecks.UI that XMPro does not use.
- [CVE-2025-10148](https://www.cve.org/CVERecord?id=CVE-2025-10148): curl WebSocket payload masking issue; XMPro uses .NET HttpClient, not curl.
- [CVE-2025-13034](https://www.cve.org/CVERecord?id=CVE-2025-13034): curl QUIC TLS key pinning issue; XMPro uses .NET HttpClient, not curl.
- [CVE-2025-13151](https://www.cve.org/CVERecord?id=CVE-2025-13151): libtasn1-6 vulnerable code never executed; XMPro uses OpenSSL not GnuTLS.
- [CVE-2025-14104](https://www.cve.org/CVERecord?id=CVE-2025-14104): util-linux setpwnam race condition; SUID utilities not used in XMPro containers.
- [CVE-2025-14524](https://www.cve.org/CVERecord?id=CVE-2025-14524): curl OAuth2 Bearer token leak; XMPro uses .NET HttpClient, not curl.
- [CVE-2025-14819](https://www.cve.org/CVERecord?id=CVE-2025-14819): curl CA certificate store caching issue; XMPro uses .NET TLS, not curl.
- [CVE-2025-15281](https://www.cve.org/CVERecord?id=CVE-2025-15281): libc-bin (glibc) requires wordexp() with WRDE_REUSE+WRDE_APPEND flags; not used by XMPro applications.
- [CVE-2025-30258](https://www.cve.org/CVERecord?id=CVE-2025-30258): gpgv certificate import DoS; XMPro doesn't import GnuPG keys.
- [CVE-2025-68972](https://www.cve.org/CVERecord?id=CVE-2025-68972): gpgv plaintext injection in signed messages; XMPro doesn't verify GPG signatures.
- [CVE-2025-68973](https://www.cve.org/CVERecord?id=CVE-2025-68973): gpgv scanner data lag; Debian shows 2.2.40-1.1+deb12u2 is already fixed.
- [CVE-2026-0861](https://www.cve.org/CVERecord?id=CVE-2026-0861): glibc requires attacker control of both size and alignment parameters; not possible in XMPro managed code.
- [CVE-2026-0915](https://www.cve.org/CVERecord?id=CVE-2026-0915): glibc requires getnetbyaddr() with zero-valued network parameter; XMPro applications don't call this function.
- [CVE-2026-2219](https://www.cve.org/CVERecord?id=CVE-2026-2219): dpkg zstd decompression infinite loop; only affects processing untrusted .deb archives, not done in XMPro containers.
- [CVE-2026-3805](https://www.cve.org/CVERecord?id=CVE-2026-3805): curl vulnerability in Debian Trixie; XMPro uses .NET HttpClient for all HTTP operations, not curl. No fix available from Debian.
- [CVE-2026-22184](https://www.cve.org/CVERecord?id=CVE-2026-22184): zlib (npm) untgz utility not present in browserify-zlib/minizlib; pure JS packages unaffected.
- [CVE-2026-24882](https://www.cve.org/CVERecord?id=CVE-2026-24882): gpgv vulnerability in tpm2daemon not included in gpgv package; gpgv is only a signature verification tool.

## Disclosure

All images were scanned on March 17, 2026 using Trivy v0.61.0 with the latest vulnerability database. All Critical and High severity findings have been investigated and confirmed as false positives. Investigation and mitigation of the remaining Medium and Low severity findings did not make the cut for the 4.6.0 release. These will be reviewed and addressed in upcoming releases as part of our ongoing security improvement process.

## Replication

To independently verify these scan results:

```bash
trivy image xmpro.azurecr.io/ad:4.6.0
trivy image xmpro.azurecr.io/ds:4.6.0
trivy image xmpro.azurecr.io/ai:4.6.0
trivy image xmpro.azurecr.io/stream-host:4.6.0
trivy image xmpro.azurecr.io/stream-host:4.6.0-bookworm-slim-python3.12
trivy image xmpro.azurecr.io/stream-host:4.6.0-alpine3.21
```

> [!NOTE]
> Results may vary depending on the Trivy version and vulnerability database date used.
