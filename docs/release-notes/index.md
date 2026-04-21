# v4.6 Release Notes

This section contains the release notes for XMPro v4.6 platform, providing information about new features, improvements, and bug fixes across all core products. Key highlights include the Streams as Connectors architecture, Stream Host Event-Level Streaming architecture, OAuth SMTP support, and security enhancements across all products.

## Known Issues

<table>
  <thead>
    <tr>
      <th width="120">Product</th>
      <th>Description</th>
      <th width="95">Reported</th>
      <th width="95">Fixed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data Stream Designer</td>
      <td>Ticket ID17421 Data Stream Designer Hangs on Publish/Unpublish: When you publish or unpublish a Data Stream, the browser occasionally becomes unresponsive and requires a page refresh to recover.</td>
      <td>v4.5.5</td>
      <td>Pending</td>
    </tr>
  </tbody>
</table>

## v4.6.0

Date Released: 13 Mar 2026

### Common

<table>
  <thead>
    <tr>
      <th width="120">Change Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Feature</td>
      <td>
        <p><b>Streams as Connectors</b>: New architecture that allows App Designer applications to use a published Data Stream as a data source.</p>
        <p>The <b>XMPro Stream Connector</b> is used in App Designer to connect to a published Data Stream, supporting read, insert, update, and delete operations. The backing Data Stream comprises a <b>XMPro Stream Listener</b>, a Connector Agent (new category), and a <b>XMPro Stream Action Agent</b>. Agent configuration values are passed directly into the connected stream at runtime by App Designer. With Connectors now available in both App Designer and Data Stream Designer, attempting to import an integration file (.xmp) into the wrong product returns a clear error identifying which product the file belongs to.</p>
        <p>Using this new feature results in much faster App Page page loads and less infrastructure to run the XMPro platform, but does require a MQTT broker to use it.</p>
        <p><i>If you are upgrading, a migration script is available to transition your existing connections. Contact your XMPro account manager for assistance.</i></p>
      </td>
    </tr>
    <tr>
      <td>Enhancement</td>
      <td>
        <p><b><a href="../technical-reference/oauth-smtp-configuration.md">OAuth SMTP Configuration Support</a></b>: Platform administrators can now configure OAuth 2.0 authentication for XMPro's outbound email notifications instead of username and password credentials.</p>
        <p>OAuth SMTP authentication is supported across all deployment methods, including the Windows Server installer, Terraform modules, and Docker (xmpro-run). Administrators can configure the OAuth client ID, client secret, and token endpoint to match their email provider's requirements.</p>
        <p>Modern email providers such as Microsoft 365 and Google Workspace are phasing out basic authentication for SMTP. OAuth support ensures XMPro's email notifications, including recommendation alerts, user invitations, and system notifications, remain fully operational in environments where basic auth has been disabled, while improving the overall security posture of your deployment.</p>
      </td>
    </tr>
    <tr>
      <td>Deployment</td>
      <td>
        <p><b>Azure Container Instance Enhancements</b>: Two improvements to Stream Host deployments using Azure Container Instances (ACI):</p>
        <ul>
          <li><b>Virtual Network Integration</b>: ACI deployments can now be connected to an Azure Virtual Network, enabling private networking without public-facing container endpoints and meeting enterprise security and compliance requirements.</li>
          <li><b>Right-Sized Default Configuration</b>: Default CPU and memory allocations have been updated to better reflect production workload requirements, reducing the need for manual configuration adjustments after initial deployment.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Security</td>
      <td>
        <p><b>Product security and stability</b>: We've addressed several security vulnerabilities in this release.</p>
        <p><i>Mitigated:</i></p>
        <ul>
          <li><a href="https://www.cve.org/CVERecord?id=CVE-2022-26907">CVE-2022-26907</a>: Upgraded Microsoft.Rest.ClientRuntime from 2.3.20 to 2.3.24 in App Designer and from 2.3.11 to 2.3.24 in Data Stream Designer.</li>
          <li><a href="https://www.cve.org/CVERecord?id=CVE-2022-34716">CVE-2022-34716</a>: Upgraded System.Security.Cryptography.Xml from 4.4.2 to 6.0.1 in App Designer.</li>
          <li><a href="https://www.cve.org/CVERecord?id=CVE-2023-29331">CVE-2023-29331</a>: Added System.Security.Cryptography.Pkcs 6.0.3 to App Designer.</li>
          <li><a href="https://www.cve.org/CVERecord?id=CVE-2025-54575">CVE-2025-54575</a>: Upgraded SixLabors.ImageSharp from 3.1.7 to 3.1.11 in App Designer and Data Stream Designer.</li>
          <li><a href="https://github.com/advisories/GHSA-4vgm-c2wm-63mw">GHSA-4vgm-c2wm-63mw</a>: Upgraded Microsoft.AspNetCore.App.Runtime.linux-musl-x64 from 8.0.24 to 8.0.25 in Subscription Manager, App Designer, Data Stream Designer, and XMPro AI.</li>
          <li>Removed unused npm dependencies and overrode transitive package versions in App Designer to resolve Veracode-identified vulnerabilities in tar and tsiclient.npm.</li>
          <li><a href="https://cwe.mitre.org/data/definitions/117.html">CWE-117</a>: Applied log output sanitization to neutralize CRLF injection in App Designer and Data Stream Designer.</li>
          <li><a href="https://cwe.mitre.org/data/definitions/285.html">CWE-285</a>: Added class-level [Authorize] attributes in App Designer and Data Stream Designer to enforce authentication by default, with explicit [AllowAnonymous] exemptions for public endpoints such as error pages and silent token renewal.</li>
        </ul>
        <p>For false positive assessments and container scan results, see the <a href="../resources/container-scan-4-6-0.md">Container Security Scan Report - XMPro 4.6.0</a>.</p>
      </td>
    </tr>
  </tbody>
</table>

### Data Stream Designer

<table>
  <thead>
    <tr>
      <th width="120">Change Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Fix</td>
      <td><b>DropDown and TokenBox Not Displaying When Options Array Is Empty</b>: <i>When a DropDown or TokenBox property on an agent is configured with an empty options array, the control does not render in the agent configuration panel, making the property inaccessible.</i><br>DropDown and TokenBox controls now render correctly regardless of whether the options array is empty at the time the configuration panel is opened.</td>
    </tr>
  </tbody>
</table>

### Stream Host

<table>
  <thead>
    <tr>
      <th width="120">Change Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Feature</td>
      <td>
        <p>This release introduces a set of improvements that together deliver a more reliable, efficient, and upgrade-friendly Stream Host:</p>
        <ul>
          <li><b>Memory Optimisation</b>: Rearchitected with Event-Level Streaming Architecture, processing data one event at a time through a chain of agents rather than accumulating large in-memory batches.
  <ul>
  <li>Each agent releases memory as soon as it forwards an event, preventing unnecessary retention of intermediate results and significantly reducing RAM usage.</li>
  <li>Downstream agents begin processing immediately upon receiving each event, without waiting for the full batch from the preceding agent.</li>
  <li>Supports both event-level and batch processing: Event-Level Streaming for agents that can process each event independently and Agent-Level Streaming retained for agents that require full datasets (e.g. time-series for model-based analysis).</li>
  </ul>
  </li>
          <li><b>Backward Compatibility</b>: Event-Level Streaming-enabled agents can run on pre 4.6 Stream Host instances, enabling rolling upgrades without downtime, but they will revert to Agent-Level Streaming behavior.</li>
          <li><b>Process Isolation</b>: Errors in a data stream are contained and no longer affect other streams running on the same Stream Host instance.</li>
          <li><b>Stable Assembly Versions</b>: Agent DLLs now maintain a consistent assembly version across builds, so developers no longer need to recompile custom agents after a Stream Host update.</li>
        </ul>
        <p>Process isolation and some memory improvements apply immediately without any changes to existing agents. To take full advantage of Event-Level Streaming, agents must be updated to implement the new async methods and overloads - see XMPro.IOT.Framework under NuGet Packages below.</p>
      </td>
    </tr>
  </tbody>
</table>

### Subscription Manager

No changes in this release.

### Package Manager

<table>
  <thead>
    <tr>
      <th width="120">Change Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Enhancement</td>
      <td><b>Connector Category Support for Agent Packaging</b>: Agents can now be packaged using the new Connector category for use in Data Stream Designer. This category supports the <b>Streams as Connectors</b> feature - see Common above.</td>
    </tr>
  </tbody>
</table>

### NuGet Packages

#### Agent Development

##### XMPro.IOT.Framework

<table>
  <thead>
    <tr>
      <th width="120">Change Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Enhancement</td>
      <td>
        <p>The following async methods and constructor overloads were added to existing interfaces and args classes to support <b>Event-Level Streaming</b> feature - see Stream Hosts above:</p>
        <ul>
          <li><code>IPollingAgent</code>: new <code>PollAsync()</code> overload for async polling.</li>
          <li><code>IReceivingAgent</code>: new <code>ReceiveAsync(string, IAsyncEnumerable&lt;byte[]&gt;)</code> overload for continuous stream ingestion.</li>
          <li><code>IMapAndReceiveAgent</code>: new <code>ReceiveAsync(string, IAsyncEnumerable<(byte[], byte[])>)</code> overload for Agents that receive a mapped/typed stream of data evenets.</li>
          <li><code>OnPublishArgs</code>: new constructors accepting <code>IAsyncEnumerable&lt;byte[]&gt;</code> and <code>IAsyncEnumerable&lt;string&gt;</code> for streaming event publishing.</li>
          <li><code>OnErrorArgs</code>: new constructor accepting <code>IEnumerable&lt;JToken&gt;</code> for streaming error data.</li>
        </ul>
        <p>Agents that do not implement the async methods and overloads continue to work without any changes.</p>
      </td>
    </tr>
  </tbody>
</table>

#### Connector Development

No changes to XMPro.Integration.Framework, XMPro.Integration.Helpers, or XMPro.Integration.Settings.
