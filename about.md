# What is SLSA?

## Principles

SLSA focuses on the following two main principles:

*   **Non-unilateral:** No person can modify the software artifact anywhere in
    the software supply chain without explicit review and approval by at least
    one other "trusted person."[^1] The purpose is prevention, deterrence,
    and/or early detection of risky/bad changes.

*   **Auditable:** The software artifact can be securely and transparently
    traced back to the original, human readable sources and dependencies. The
    primary purpose is for automated analyses of sources and dependencies, as
    well as ad-hoc investigations.

Though not perfect, these two principles provide substantial mitigation for a
wide range of tampering, confusion, and other supply chain attacks.

To measure how well protected a supply chain is according to the two principles
above, we propose the SLSA levels. A higher level means it is better protected.
SLSA 4 is the end goal but may take many years and significant investment for
large organizations. SLSA 1 through SLSA 3 are stepping stones to recognize
meaningful progress.

What sets SLSA 4 apart from simple best practices is its resilience against
determined adversaries. That is, SLSA is a **guarantee** that these practices
have been followed, though still not a guarantee that the software is "safe."

## Summary of requirements

See [Requirements](requirements.md) for details.

<!-- IMPORTANT: Keep this in sync with requirements.md. -->

<table>
 <thead>
  <tr><th colspan="2">           <th colspan="4">Required at</tr>
  <tr><th colspan="2">Requirement<th>SLSA 1<th>SLSA 2<th>SLSA 3<th>SLSA 4</tr>
 </thead>
 <tbody>
  <tr><td rowspan="4">Source
      <td>Version Controlled        <td> <td>✓<td>✓     <td>✓</tr>
  <tr><td>Verified History          <td> <td> <td>✓     <td>✓</tr>
  <tr><td>Retained Indefinitely     <td> <td> <td>18 mo.<td>✓</tr>
  <tr><td>Two-Person Reviewed       <td> <td> <td>      <td>✓</tr>
  <tr><td rowspan="7">Build
      <td>Scripted                  <td>✓<td>✓<td>✓     <td>✓</tr>
  <tr><td>Build Service             <td> <td>✓<td>✓     <td>✓</tr>
  <tr><td>Ephemeral Environment     <td> <td> <td>✓     <td>✓</tr>
  <tr><td>Isolated                  <td> <td> <td>✓     <td>✓</tr>
  <tr><td>Parameterless             <td> <td> <td>      <td>✓</tr>
  <tr><td>Hermetic                  <td> <td> <td>      <td>✓</tr>
  <tr><td>Reproducible              <td> <td> <td>      <td>○</tr>
  <tr><td rowspan="5">Provenance
      <td>Available                 <td>✓<td>✓<td>✓     <td>✓</tr>
  <tr><td>Authenticated             <td> <td>✓<td>✓     <td>✓</tr>
  <tr><td>Service Generated         <td> <td>✓<td>✓     <td>✓</tr>
  <tr><td>Non-Falsifiable           <td> <td> <td>✓     <td>✓</tr>
  <tr><td>Dependencies Complete     <td> <td> <td>      <td>✓</tr>
  <tr><td rowspan="3">Common
      <td>Security                  <td> <td> <td>      <td>✓</tr>
  <tr><td>Access                    <td> <td> <td>      <td>✓</tr>
  <tr><td>Superusers                <td> <td> <td>      <td>✓</tr>
 </tbody>
</table>

## Why do we need SLSA?

SLSA addresses three issues:

*   Software producers want to secure their supply chains but don't know exactly
    how.
*   Software consumers want to understand and limit their exposure to supply
    chain attacks but have no means of doing so.
*   Artifact signatures alone only prevent a subset of the attacks we care
    about.

At a minimum, SLSA can be used as a set of guiding principles for software
producers and consumers. More importantly, SLSA allows us to talk about supply
chain risks and mitigations in a common language. This allows us to communicate
and act on those risks across organizational boundaries.

Numeric levels, in particular, are useful because they are simple. A decision
maker easily understands that SLSA 4 is better than SLSA 3 without understanding
any of the details. That said, we are not committed to numeric levels and are
open to other options.

Once SLSA is complete it will provide a mapping from requirements that the
supply chain can implement to the attacks they can prevent. Software producers
and consumers will be able to look at the SLSA level of a software artifact and
know what attacks have been defended against in its production.

## Related work

In parallel to the SLSA specification, there is work to develop core formats and
data models. Currently this is joint work between
[Binary Authorization](https://cloud.google.com/binary-authorization) and
[in-toto](https://in-toto.io/) but we invite wider participation.

*   [Standard attestation format](https://github.com/in-toto/attestation#in-toto-attestations)
    to express provenance and other attributes. This will allow sources and
    builders to express properties in a standard way that can be consumed by
    anyone. Also includes reference implementations for generating these
    attestations.
*   Policy data model and reference implementation.

For a broader view of the software supply chain problem:

*   [Know, Prevent, Fix: A framework for shifting the discussion around
    vulnerabilities in open
    source](https://security.googleblog.com/2021/02/know-prevent-fix-framework-for-shifting.html)
*   [Threats, Risks, and Mitigations in the Open Source Ecosystem]

Prior iterations of the ideas presented here:

*   [Building Secure and Reliable Systems, Chapter 14: Deploying Code](https://sre.google/static/pdf/building_secure_and_reliable_systems.pdf#page=339)
*   [Binary Authorization for Borg] - This is how Google implements the SLSA
    idea internally.

Other related work:

*   [CII Best Practices Badge](https://bestpractices.coreinfrastructure.org/en)
*   [Security Scorecards](https://github.com/ossf/scorecard) - Perhaps SLSA
    could be implemented as an aggregation of scorecard entries, for at least
    the checks that can be automated.
*   [Trustmarks](https://trustmark.gtri.gatech.edu/)

Other takes on provenance and CI/CD:

*   [The Path to Code Provenance](https://medium.com/uber-security-privacy/code-provenance-application-security-77ebfa4b6bc5)
*   [How to Build a Compromise-Resilient CI/CD](https://www.youtube.com/watch?v=9hCiHr1f0zM)

## Footnotes

[^1]: "Trusted person" is defined by the organization or developers that
    own/produce the software. A consumer must ultimately trust them to do the
    right thing. The non-unilateral principle protects against individuals
    within the organization subverting the organization's goals.

<!-- Links -->

[Binary Authorization for Borg]: https://cloud.google.com/security/binary-authorization-for-borg
[Threats, Risks, and Mitigations in the Open Source Ecosystem]: https://github.com/Open-Source-Security-Coalition/Open-Source-Security-Coalition/blob/master/publications/threats-risks-mitigations/v1.1/Threats%2C%20Risks%2C%20and%20Mitigations%20in%20the%20Open%20Source%20Ecosystem%20-%20v1.1.pdf
[feedback form]: https://forms.gle/93QRfUqF7YY2mJDi9
[mailing list]: https://groups.google.com/g/slsa-discussion
