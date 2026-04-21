# Platform Security

XMPro places a high priority on security, performing app security checks every 3 months using Veracode. Veracode's comprehensive analysis helps identify, prevent, and fix vulnerabilities through multiple testing methods: Static Analysis (white-box testing), Dynamic Analysis (black-box testing), and Software Composition Analysis.

## Security Technologies and Practices

Our suite of products leverages robust technologies and practices to maintain a high security standard:

* **App Designer**, **Data Stream Designer**, and **XMPro AI** are built on **dotnet 8**.
* **Subscription Manager** is built on Microsoft .NET Framework 4.8 Runtime.

In the event a vulnerability is identified in any of these technologies, Microsoft promptly releases an update. We integrate these updates into our products and regularly release new versions that include essential security fixes.

### Static Application Security Testing (SAST)

Static Application Security Testing (SAST) is a form of white-box testing used to scan an application's source, binary, or byte code.

### Dynamic Application Security Testing (DAST)

Dynamic Application Security Testing (DAST) analyzes a web application through the front end to find vulnerabilities through simulated attacks. This is also called Penetration testing.

### Software Composition Analysis (SCA)

Software Composition Analysis scans all the components used in an application for security risks and vulnerabilities.

## Application Security Results

| Product | SAST Score | DAST Score | Date |
| --- | --- | --- | --- |
| Subscription Manager 4.6.0 | 98 | 94 | 18 Mar 26 |
| App Designer 4.6.0 | 95 | 95 | 18 Mar 26 |
| Data Stream Designer 4.6.0 | 99 | 95 | 18 Mar 26 |
| XMPro AI 4.6.0 | 95 | 95 | 18 Mar 26 |
| WorkFlow | 95 | 95 | 18 Mar 26 |

## Container Security Scanning

In addition to application-level security testing, XMPro performs container image vulnerability scanning on every release using [Trivy](https://trivy.dev/), an open-source vulnerability scanner. All container images published to the XMPro Azure Container Registry are scanned for known vulnerabilities in OS packages and application dependencies.

Each scan report includes:

* Vulnerability counts by severity (Critical, High, Medium, Low)
* False positive analysis for all Critical and High findings
* Affected packages and CVE identifiers
* Replication commands for independent verification

### Container Scan Reports

| Version | Scan Date | Scanner | Images Scanned | Report |
|---------|-----------|---------|----------------|--------|
| 4.6.0 | 17 Mar 26 | Trivy v0.61.0 | 6 | [View Report](container-scan-4-6-0.md) |

## Support and Recommendations

.NET versions are supported by Microsoft for 3 years after release, as detailed in their [support policy](https://dotnet.microsoft.com/en-us/platform/support/policy). To ensure you have the most secure XMPro offerings, we recommend upgrading at least every 3 months to take advantage of the latest security updates and features.
