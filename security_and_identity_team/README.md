# Security and Identity Team

<p align="center">
<img src="images/venn.png" alt="Security and Identity" width="400"/>
</p>



When Privacy-Preserving Machine Learning (PPML) arrives into the mainstream, the effects will be felt in every sector of the data industry. We aim to help the AI community brace for impact by exploring the still uncharted area around security appraisal, trust and governance mechanisms relating to PPML.

## Our roadmap for 2020

<details><summary><b>COVID-19 Self-Sovereign Identity (SSI)</b></summary>
<p>
We aim to create free education and tools aimed at onboarding COVID app developers into working with self-sovereign identity (SSI) principles:

- We are working with the writing team to create free education around SSI.
- We are working on a branch of Opus, which will extend Opus with full SSI credential creation, issuance, verification and revocation functionality. This will ultimately allow Opus to provide SSO services upon the receipt of valid proofs from a user relating to that particular identity; no further information is required.
- We are working with the Sovrin foundation as a greater community on establishing credential and governance standards for dealing with the swathes of data surrounding COVID. We are building standard tooling for working with the established data types.

<a href="./projects/COVID-SSI/COVID-SSI.md">An overview of this project can be seen here.</a>
</p>
</details>

<details><summary><b>Recommendation of Standard Governance Frameworks for PPML</b></summary><p>
Governance models are important because they bridge the gap between what is possible and what is legislatively justifiable. Businesses need to know why PPML is important, why it's going to save them resources in information security management and, most importantly, how they can justify it to their auditor. To this end we are working on recommendations and documenation around the following:<br><br>

- Recommendation of incident response standard guidelines concerning PPML security incidents<br>
- Exploring appropriate design ethics for privacy-preserving systems<br>
- Exploring PPML feasability with respect to existing legislative requirements (GDPR, HIPAA)<br>
- PPML Risk Management Exploration and Documentation<br>
- Integration and assimilation with existing InfoSec Standards (ISO 27000, NIST)<br>
- Recommendation of Standard PPML Security<br>
</p>
</details>

<details><summary><b>Documentation and Security Audit of Privacy-preserving Tools and Workflows</b></summary><p>

There are existing tools and workflows in PySyft which have never been used in industry. It's our obligation before recommending the use of these tools to first explore them with a sceptical eye. Under this objective, we develop documentation surrounding tools including their known applications, privacy and security constraints and resource constraints. We are exploring tools under the following taxonomical branches:

- PPML Differential Privacy Mechanisms <br>
- PPML Cryptographic mechanisms <br>
- PPML through Distribution of Information Assets
- Distributed Identity and Trust Mechanisms for PPML
</p>

</details>

<details><summary><b>Appraisal and Documentation of Existing Attacks on Learning Models</b></summary>
<p>

Privacy-preserving techniques distribute computation in order to ensure that data remains in the control of the owner while learning takes place. However, architectures distributed amongst multiple agents introduce an entirely new set of security and trust complications. These include data poisoning and model theft.

We work on documenting and creating free education materials for attacks on AI applications. We do this with the intention of raising awareness amongst the community who are implementing applications, In turn this should encourage best practices.
<p>
</details>


<details><summary><b>Application Level Architecture Documentation and Security Audit</b></summary>

We will be working with the Syft team, Web and Mobile team and the PyGrid team to create architecture documentation and monitor dependencies for vulnerabilities and apply recommended information governance systems.  
</details>

<details><summary><b>Network Level ArchitectureDocumentation and Security Audit </b></summary>

We perform security audit on live hosts running Grid services as well as demonstrate leakage network captures on post-mortem data. We use these experiments to monitor for leakage in the OM stack and provide ammunition for forensics or CTF challenges.

</details>

<details><summary><b>CTF, Forensics and Performance Challenges</b></summary>

We aim to organise events around breaking and improving upon our tools. These fall under the following categories:

- Live CTF network-based Attacks
- Forensics Challenges
- Bug-bounties
- Performance Optimisation Challenges
</details>

<details><summary><b>SplitNN Standard Class Type Development and Hardening against Information Leakage</b></summary>

Traditionally, PySyft has been used to facilitate federated learning. However, we can also leverage the tools included in this framework to implement distributed neural networks. These allow for researchers to process data held remotely and compute predictions in a radically decentralised way. First introduced by MIT in December 2018, SplitNNs represent a brand new architectural mechanic for privacy-preserving ML researchers to play with. <b> We have built the worlds first fully open-source implementation of Split Neural Networks. </b>

While SplitNNs are an interesting architectural development, they are far from being a secure distributed learning method. The issues here are documented in <b><a href="documentation/tools/DoIA/SplitNN/VulnA.pdf">vulnerability A </a></b> and <b><a href="documentation/tools/DoIA/SplitNN/VulnB.pdf"> vulnerability B</a></b>. We are currently working on methods to counter these vulnerabilities.

</details>

<details><summary><b>PyGrid SSI Integration</b></summary>

We aim to use Hyperledger Aries as a mechanism to facilitate trust in PyGrid. More details to come.

</details>

<details><summary><b>Zero-Knowledge Data Discovery and Transport (ZK-Alexandria)</b></summary>

##### <u>Get in touch if you'd like to know more about this project!</u>

<img src="images/200.gif" alt="ZK-Alexandria" width="300"/>

</details>

<details><summary><b>Design PySyft Data Object Access Control Mechanism</b></summary>
We will be working with the PySyft team to desing an implement an object access management system.  
</details>





## Team Members

The team leader is [**Adam James Hall**](https://github.com/H4LL). Our team is comprised of the following people.

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/H4LL">
        <img src="https://avatars1.githubusercontent.com/u/46713492?s=240" width="170px;" alt="Adam James Hall">
        <br /><sub><b>Adam James Hall</b></sub></a><br />
        <sub>Team Lead</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/LaRiffle">
        <img src="https://avatars3.githubusercontent.com/u/12446521?s=240" width="170px;" alt="Théo Ryffel">
        <br /><sub><b>Théo Ryffel</b></sub></a><br />
        <sub>PPML + Cryptography</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/wip-abramson">
        <img src="https://avatars1.githubusercontent.com/u/18055112?s=460&u=8542a349dfdd82110c7c66f8168f6236337b646a&v=4" width="170px;" alt="">
        <br /><sub><b>Will Abramson</b></sub></a><br />
        <sub>Self-Sovereign Identity</sub>
      </a>
    </td>
  </tr>
  <tr>
  <td align="center">
    <a href="https://github.com/pavlos-p">
      <img src="https://avatars0.githubusercontent.com/u/44439128?s=460&u=eb02441a2d6cfd14d47d7afb13847a60c6e531ba&v=4" width="170px;" alt="">
      <br /><sub><b>Pavlos Papadopoulos</b></sub></a><br />
      <sub>PPML + Security Audit</sub>
    </a>
  </td>
    <td align="center">
      <a href="https://github.com/tremblerz">
        <img src="https://avatars3.githubusercontent.com/u/10557215?s=460&u=c7601df5ccc1ded707d8d05aa161c1a9fb39c604&v=4" width="170px;" alt="">
        <br /><sub><b>Abhishek Singh</b></sub></a><br />
        <sub>Split Neural Networks</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/FarrandTom">
        <img src="https://avatars3.githubusercontent.com/u/33008723?s=460&u=96c52f512622acdb4ab4b7396e348c45bdcbfe28&v=4" width="170px;" alt="">
        <br /><sub><b>Tom Farrand</b></sub></a><br />
        <sub>Privacy-Preserving ML</sub>
      </a>
    </td>
  </tr>
  <tr>    
  <td align="center">
        <a href="https://github.com/JulianSprung">
          <img src="https://avatars3.githubusercontent.com/u/36044639?s=460&u=e2cfedf5c7282096990b214d8f021d5f56145245&v=4" width="170px;" alt="">
          <br /><sub><b>Julian Sprung</b></sub></a><br />
          <sub>Security + Performance Challenges</sub>
        </a>
      </td>
  <td align="center">
    <a href="https://github.com/youben11">
      <img src="https://avatars0.githubusercontent.com/u/21220087?s=240" width="170px;" alt="">
      <br /><sub><b>Ayoub Benaissa</b></sub></a><br />
      <sub>CrypTen integ. + TenSEAL</sub>
    </a>
  </td>
    <td align="center">
      <a href="https://github.com/setiadeepanshu">
        <img src="https://avatars3.githubusercontent.com/u/13046972?s=460&u=ae6b5b6b64a1baead6a6490c0b605290062a857e&v=4" width="170px;" alt="">
        <br /><sub><b>Deepanshu Setia</b></sub></a><br />
        <sub>Privacy-Preserving ML</sub>
      </a>
    </td>
  </tr>  
  <tr>
  <td align="center">
    <a href="https://github.com/ttitcombe">
      <img src="https://avatars0.githubusercontent.com/u/32938439?s=460&u=0087d99ceab10ba55b055a8ce3f722dac6829b24&v=4" width="170px;" alt="">
      <br /><sub><b>Tom</b></sub></a><br />
      <sub>Privacy-Preserving ML</sub>
    </a>
  </td>
  <td align="center">
    <a href="https://github.com/40415056">
      <img src="https://avatars3.githubusercontent.com/u/47462996?s=460&u=e2507ee0bbcaaf0a75fdf5792856607756c69edc&v=4" width="170px;" alt="">
      <br /><sub><b>Afzaal Hussain</b></sub></a><br />
      <sub>Information Security Governance</sub>
    </a>
  </td>
  </tr>
</table>

## Projects

Learn more about our projects:

<details><summary><a href="https://github.com/OpenMined/PySyft/tree/master/examples/tutorials/advanced/split_neural_network"><b>Open-source</b> implementation of <b>Split Neural Networks</b> </a></summary>
</details>
<details><summary><a href="./projects/COVID-SSI/COVID-SSI.md">COVID-19 Open-Source SSI Project</a></summary>
</details>
<details><summary><a href="https://github.com/OpenMined/aries-fl">A Distributed Trust Framework for Privacy Preserving Machine Learning</a></summary>
</details>
<details><summary>ZK-Alexandria</summary>
<p>
More coming soon...
</p>
</details>


<!-- ## Weekly Meetings

We have weekly meetings that are currently private, [but we take detailed notes for each meeting](./meetings). Here you can will find our weekly status updates: where each member of our team has recorded what they worked on the previous week and what they plan to work on in the upcoming week. -->

<!-- ## Contact

### Want to join?

If you're already a contributor to PySyft, and if you're interested to to work on crypto related use cases, you should definitely join us!

*[Apply to the crypto team!](https://docs.google.com/forms/d/1T6MJ21V1lb7aEr4ilZOTYQXzxXP6KbpLumZVmTZMSuY/edit)* -->

### Looking for a Project?

<b><a href="workmap.pdf"> Feel free to run with anything on our Workmap!</a></b>

### Have questions?
- [**@Adam J Hall** on Slack](https://app.slack.com/client/T6963A864/C69RB18LA/user_profile/UFQ4YUPMJ)
- [**@Adam James Hall** on Linkedin](https://www.linkedin.com/in/adam-james-hall-1b0229113/)
- [**@AJH4LL** on Twitter](https://twitter.com/AJH4LL)
- <b>Email: Adam@napier.ac.uk </b>
