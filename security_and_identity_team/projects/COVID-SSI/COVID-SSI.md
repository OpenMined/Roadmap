# COVID Self-Sovereign Identity (SSI)

### Objectives

- To provide <b>free-education around SSI </b> to COVID app makers.
- To provide <b>open-source SSI tools</b> for COVID App makers to use.

## Free Education


We will be working with the writing team at OpenMined to create blog posts aimed at lowering the barrier of entry into SSI for developers. If you'd like to write a blogpost, reach out on the Slack! We are also working with members of the Sovrin foundation to produce useful learning material.




<details><summary><b>SSI Projects Around COVID-19</b></summary>

<b>COVI-ID</b><br>
<a href="https://medium.com/coviid/covi-id-privacy-preserving-covid-19-status-verification-c11d59ec92f6">The COVI-ID SSI Project</a>
Covi-ID is a South African led consortium building a similar proof of health application as SafePass using SSI. This supports a flow where a single scan of a QrCode can act as proof of status.
</details>

<details><summary><b>SSI Tools</b></summary>
<b>StreetCred</b>

StreetCred is an SSI as a service organisation aimed at lowering the barrier of entry to SSI. An Introduction to the StreetCred tools and SSI more generally <a href="https://docs.streetcred.id/docs/getting-started"> can be found here.</a>
</details>

<details><summary><b>SSI Concepts</b></summary>
- <a href="https://player.vimeo.com/video/305420834?title=0&amp;byline=0"> What is SSI?</a> <br>
- <a href="https://misterwip.uk/cl-signatures">CL Signatures</a>
</details>

<details><summary><b>The Sovrin Foundation</b></summary>
</details>

### Do you have any specific questions you'd like answered?<br> <a href="https://docs.google.com/document/d/1_A9_M9clVvFSs10UTitvEVGaBP4K4efUiOj7ls7nFXI/edit?usp=sharing"> Write them here.</a>


## Open Source Tools

The technical branch of this project is to extend <a href="https://github.com/OpenMined/private-identity-server">Opus</a> with SSI functionality like token issuance and verification. Once this is established, we can run <a href="https://github.com/OpenMined/private-identity-server">Opus</a> SSO services purely on the basis of the proof certificates provided by users,
In the long term we can also use this to aggregate information from online identities and issue these attributes as verifiable credentials to <a href="https://github.com/OpenMined/private-identity-server">Opus</a> users. This allows users to participate in other SSI learning applications with information that has previously been verified and attested to by <a href="https://github.com/OpenMined/private-identity-server">Opus</a>. We can use <a href="https://misterwip.uk/cl-signatures">CL Signatures</a> to allow users to prove their data is 'correct' without a remote SSI application ever knowing its value. The remote SSI application can send their model to the user to learn their data. If, as <a href="https://github.com/OpenMined/private-identity-server">Opus</a>, we also issue noised data credentials then we can train differentially private models on verifiably correct data which never leaves the control of the user.

<img src="images/endgame.png " alt="SSI Open Data Market" width="1000"/>


However, to begin with, we're not going that deep. We want to be able to provide Single-Sign-On (SSO) services to anyone who presents valid credentials for doing so. That means <a href="https://github.com/OpenMined/private-identity-server">Opus</a> hardly needs to store any information about it's users. All it needs to know when vouching for users to third-party organisations is the bare minimum and that can be verified through credentials presnted by the user at the time of requesting that service, not necessarily database.If <a href="https://github.com/OpenMined/private-identity-server">Opus</a> has previously signed off the valid credential, it's as good as it being taken from database controlled by <a href="https://github.com/OpenMined/private-identity-server">Opus</a>. To achieve this integration we are doing two projects things in parallel:

### A - SSI Open-Source (ETA: 3 months).
<img src="images/PlanA.png " alt="Long Term" width="1000"/>

<b>Development Lead: [Pavlos Papadopolous](https://github.com/pavlos-p)</b>

In the long-run, we want a completely open-source solution for SSI compatibility in order to catalyse adoption. However, creating controller logic in Opus for a HL-Aries agent is a non-trivial task. There is not due to incompletion of the backing technology. There is little surrounding documentation and a massive skill gap in the privacy community. Plan A is to implement generic, open-source Agent controller logic to be used in Opus for an application performing abitrary SSI flows.  

### B - SSI StreetCred (ETA: 14 days).
<img src="images/PlanB.png " alt="Short Term" width="1000"/>

<b>Development Lead: [Tom Farrand](https://github.com/FarrandTom)</b><br>
<b>Project Repo: <a href="https://github.com/OpenMined/private-identity-server/tree/ssi-streetcred">SSI StreetCred</a></b>


We need a solution as soon as possible. To this end we will develop a solution using existing <a href="https://developer.streetcred/">StreetCred</a> software. <a href="https://developer.streetcred/">StreetCred</a> provide a well documented closed-source controller for Aries. This will allow us to create a proof of concept extremely quickly. If this is your first project with SSI, this project is good because you can read all of the <a href="https://docs.streetcred.id/docs/getting-started">free education</a> already created around SSI by the <a href="https://developer.streetcred/">StreetCred</a> team.


<b>Flow Diagrams:</b>

- <b><a href="B/create-account.pdf">Flow 1: Create an Account</a>
- <a href="B/login-ssi.pdf">Flow 2: Log in to Account for SSO Services</a></b>


### C - SSI Governance (ETA: Ongoing)

<b>Project Lead: <a href="https://github.com/wip-abramson">Will Abramson</a></b><br>
<b>Working Document: <a href="https://docs.google.com/document/d/1FBnIWrHpbuGFwA1eZybPz-J1QNA9KKpGAC5sl3-BEZs/edit?usp=sharing">Governance Authority Requirements
</a></b>

This is a suggestion for a workstream as part of the Covid19Credentials initiative to develop an open source tool for a Governance Authority within a domain specific governance framework.

This tool should enable the easy initialisation of a credential ecosystem and support machinable rules defined as part of the Governance Framework which can be easily and securely disseminated to participants within the system without compromising privacy.

The question that drives this proposal is:
How might we develop tools to enable machinable rules that govern a credential ecosystem such that Verifiers and Holders can have high confidence in an issuer's authority?


## Want to Get Started? <a href="https://join.slack.com/share/I01165ND7U3/VL60LnfUIXEZ0sOav30G5Am9/enQtMTA0MDE5MjQ0OTk1NS05ZDU2ZjYwYzNkZWRiMmMyNzgxMjFkOGQ5ZGQ5NzU1M2E2ODhhNTFlZjE3ZGQ0ZGM1NmNhZGU1MzIxZmU5NTk2">Join our Slack. </a>

### Author

Adam J Hall - Twitter: [@AJH4LL](https://twitter.com/AJH4LL) · GitHub: [@H4LL](https://github.com/H4LL)
