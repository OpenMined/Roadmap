# Crypto Team

## Our current projects

<details><summary><b>Integration of <a href="./projects/CrypTen.md">Crypten in PySyft</a></b></summary>
<p>
We're also working on integrating the CrypTen library for MPC which is developed by Facebook. This is a top priority project of the team, and will allow users to benefit from the massive optimizations of this library which works only with PyTorch.
</p>
</details>

<details><summary><b>Integration of SEAL in ML with <a href="https://github.com/OpenMined/tenseal">TenSEAL</a></b></summary>
<p>
We currently support standard protocols in MPC but would like to extend support for Homomorphic Encryption and other protocols (like Functional Encryption), to allow researchers to use any of them and to compare them for their usecase. In particular, we will provide support for the 1st class HE library SEAL built by Microsoft, through a dedicated library named TenSEAL which adds the abstraction of Tensor on top of SEAL. This will be DL framework agnostic.
<b>Read the <a href="./projects/TenSEAL.md">project Roadmap</a>!</b>
</p>
</details>

<details><summary><b>Integration of the Function Secret Sharing protocol</b></summary>
<p>
We're still integrating new crypto protocols natively in PySyft. This allows us to use them in a wider set of contexts, especially on mobiles and across all kind of computation frameworks. Among the next protocols we are working on Function Secret Sharing which is used in MPC to reduce the number of interactions compared to previous state-of-the-art MPC protocols. Checkout the progress <a href="https://github.com/OpenMined/PySyft/milestone/12">here</a>!
</p>
</details>

<details><summary><b>Integration of Functional Encryption</b></summary>
<p>
We're still integrating new crypto protocols natively in PySyft, including Functional Encryption, which allows to compute over encrypted data and do the decryption without any interaction! More info here: https://github.com/OpenMined/PySyft/issues/3108. 
</p>
</details>

<details><summary><b>Integration of the FALCON protocol</b></summary>
<p>
We're still integrating new crypto protocols natively in PySyft, including FALCON, an optimized version of SecureNN! Checkout the progress <a href="https://github.com/OpenMined/PySyft/milestone/13">here</a>!
</p>
</details>

<details><summary><b>Development of Encrypted NLP with <a href="https://github.com/OpenMined/SyferText">SyferText</a></b></summary>
<p>
Text processing in Federated Learning is an under-estimated complex task. We're building a library to help users clean and process remote text datasets through various methods like tokenization, etc. This library is inspired from Spacy to deliver the same user-friendly interface, and will be 100% compatible with PySyft.
</p>
</details>

<details><summary><b>Usecase: Encrypted Training on ImageNet</b></summary>
<p>
Closely related to our focus on production, we want to demonstrate the utility of the crypto protocols that we build or integrate, by building a encrypted training usecase on a more ambitious dataset than MNIST, our ideal target is for example ImageNet.
</p>
</details>

## Team Members

The team leader is [**Théo Ryffel**](https://github.com/LaRiffle). Our team is comprised of the following people.

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/LaRiffle">
        <img src="https://avatars3.githubusercontent.com/u/12446521?s=240" width="170px;" alt="Théo Ryffel">
        <br /><sub><b>Théo Ryffel</b></sub></a><br />
        <sub>Team Lead</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/gmuraru">
        <img src="https://avatars1.githubusercontent.com/u/7805588?s=240" width="170px;" alt="">
        <br /><sub><b>George Muraru</b></sub></a><br />
        <sub>CrypTen integration</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/youben11">
        <img src="https://avatars0.githubusercontent.com/u/21220087?s=240" width="170px;" alt="">
        <br /><sub><b>Ayoub Benaissa</b></sub></a><br />
        <sub>CrypTen + TenSEAL</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/AlanAboudib">
        <img src="https://avatars1.githubusercontent.com/u/11991643?s=240" width="170px;" alt="">
        <br /><sub><b>Alan Aboudib</b></sub></a><br />
        <sub>SyferText</sub>
      </a>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://github.com/Yugandhartripathi">
        <img src="https://avatars2.githubusercontent.com/u/32102845?s=240" width="170px;" alt="">
        <br /><sub><b>Yugandhar Tripathi</b></sub></a><br />
        <sub>Encrypted ML</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/sukhadj">
        <img src="https://avatars0.githubusercontent.com/u/25997368?s=460" width="170px;" alt="">
        <br /><sub><b>Sukhad Joshi</b></sub></a><br />
        <sub>Encrypted ML</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/Syzygianinfern0">
        <img src="https://avatars2.githubusercontent.com/u/31875325?s=460" width="170px;" alt="">
        <br /><sub><b>S P Sharan</b></sub></a><br />
        <sub>Core dev in SMPC</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/IamRavikantSingh">
        <img src="https://avatars2.githubusercontent.com/u/40258150?s=460&v=4" width="170px;" alt="">
        <br /><sub><b>Ravikant Singh</b></sub></a><br />
        <sub>Homomorphic Encryption</sub>
      </a>
    </td>  
  </tr>
  <tr>
    <td align="center">
      <a href="https://github.com/philomath213">
        <img src="https://avatars3.githubusercontent.com/u/20177422?s=460" width="170px;" alt="">
        <br /><sub><b>Bilal Retiat</b></sub></a><br />
        <sub>TenSEAL</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/andrelmfarias">
        <img src="https://avatars2.githubusercontent.com/u/43521764?s=240" width="170px;" alt="">
        <br /><sub><b>André Farias</b></sub></a><br />
        <sub>Encrypted Lin. Reg.</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/ajnovice">
        <img src="https://avatars3.githubusercontent.com/u/3927652?s=240" width="170px;" alt="">
        <br /><sub><b>Ajay Singh</b></sub></a><br />
        <sub>CrypTen integration</sub>
      </a>
    </td>    
    <td align="center">
      <a href="https://github.com/jasopaum">
        <img src="https://avatars2.githubusercontent.com/u/19286277?s=240" width="170px;" alt="">
        <br /><sub><b>Jason Paumier</b></sub></a><br />
        <sub>Plans + Protocols</sub>
      </a>
    </td>
</tr>
<tr>
    <td align="center">
      <a href="https://github.com/H4LL">
        <img src="https://avatars1.githubusercontent.com/u/46713492?s=240" width="170px;" alt="">
        <br /><sub><b>Adam James Hall</b></sub></a><br />
        <sub>SplitNN</sub>
      </a>
    </td>
  </tr>
</table>

## Projects

Learn more about our projects!

<details><summary><a href="./projects/CrypTen.md">CrypTen integration roadmap</a></summary>
<p>
  <a href="./projects/CrypTen.md">Go to the roadmap</a>
</p>
</details>
<details><summary><a href="https://github.com/OpenMined/SyferText">SyferText</a></summary>
<p>
  <a href="https://github.com/OpenMined/Roadmap/tree/master/nlp_team">Go to the roadmap</a>
</p>
</details>
<details><summary><a href="./projects/TenSEAL.md">TenSEAL roadmap</a></summary>
<p>
  <a href="./projects/TenSEAL.md">Go to the roadmap</a>
</p>
</details>
<details><summary>Function Secret Sharing</summary>
<p>
  <a href="https://github.com/OpenMined/PySyft/pull/3057/">See initial draft</a>
</p>
</details>


## Weekly Meetings

We have weekly meetings that are currently private, [but we take detailed notes for each meeting](./meetings). Here you can will find our weekly status updates: where each member of our team has recorded what they worked on the previous week and what they plan to work on in the upcoming week.

## Contact

### Want to join?

If you're already a contributor to PySyft, and if you're interested to to work on crypto related use cases, you should definitely join us!

*[Apply to the crypto team!](https://docs.google.com/forms/d/1T6MJ21V1lb7aEr4ilZOTYQXzxXP6KbpLumZVmTZMSuY/edit)*

### Have questions?
- [**@Théo Ryffel** on Slack](https://app.slack.com/client/T6963A864/C69RB18LA/user_profile/UA2LD4PHS)
- [**@theo-ryffel** on Linkedin](https://www.linkedin.com/in/theo-ryffel/)
- [**@theoryffel** on Twitter](https://twitter.com/theoryffel)
- Email: theo [at] openmined.org
