# Cryptography Team

Welcome to the cryptography team!

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
We're still integrating new crypto protocols natively in PySyft, including FALCON, an optimized version of SecureNN! Checkout the progress <a href="https://github.com/OpenMined/PySyft/milestone/14">here</a>!
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

## Teams

The cryptography teams are coordinated by [**Théo Ryffel**](https://github.com/LaRiffle).

### [Secure Multi-Party Computation](./smpc)

This team is led by [**George Muraru**](https://github.com/gmuraru)

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/gmuraru">
        <img src="https://avatars1.githubusercontent.com/u/7805588?s=240" width="170px;" alt="">
        <br /><sub><b>George Muraru</b></sub></a><br />
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/LaRiffle">
        <img src="https://avatars3.githubusercontent.com/u/12446521?s=240" width="170px;" alt="Théo Ryffel">
        <br /><sub><b>Théo Ryffel</b></sub></a><br />
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/AlanAboudib">
        <img src="https://avatars1.githubusercontent.com/u/11991643?s=240" width="170px;" alt="">
        <br /><sub><b>Alan Aboudib</b></sub></a><br />
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/Yugandhartripathi">
        <img src="https://avatars2.githubusercontent.com/u/32102845?s=240" width="170px;" alt="">
        <br /><sub><b>Yugandhar Tripathi</b></sub></a><br />
      </a>
    </td>
    </tr>
    <tr>
    <td align="center">
      <a href="https://github.com/aanurraj">
        <img src="https://avatars0.githubusercontent.com/u/28955148?s=460&u=b89b14ceffb4e0c26fcdc375242b3d3162700fb4&v=4" width="170px;" alt="">
        <br/><sub><b>Anubhav Raj Singh</b></sub/</a><br/>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/arturomf94">
        <img src="https://avatars2.githubusercontent.com/u/9259160?s=400&u=a363b29339e611e13e1f71ea7552e8bf5914cf37&v=4" width="170px;" alt="">
        <br/><sub><b>Arturo Marquez Flores</b></sub/</a><br/>
      </a>
    <td align="center">
      <a href="https://github.com/tudorcebere">
        <img src="https://avatars3.githubusercontent.com/u/31571425?s=460&u=250780102a5da2711faba8120fa8ab2b97c48fc9&v=4" width="170px;" alt="">
        <br/><sub><b>Tudor Cebere</b></sub></a><br/>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/abogaziah">
        <img src="https://avatars3.githubusercontent.com/u/33666625?s=460&u=1beaa9853113bc0ff6d040f3ba8a0fedc1acd17f&v=4" width="170px;" alt="">
        <br/><sub><b>Muhammed Abogazia</b></sub></a><br/>
      </a>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://github.com/abogaziah">
        <img src="https://avatars3.githubusercontent.com/u/2446179?s=460&u=56801fbae185bb7f58d339d0a4fc4288f0ab697f&v=4" width="170px;" alt="">
        <br/><sub><b>Omer Shlomovits</b></sub></a><br/>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/omershlo">
        <img src="https://avatars0.githubusercontent.com/u/39186433?s=460&u=eabfd79a99109239b61412089f86f83cc2bacf0b&v=4" width="170px;" alt="">
        <br/><sub><b>Wansoo Kim</b></sub></a><br/>
      </a>
    </td>
  </tr>
</table>

### [Homomorphic Encryption](./he)

This team is led by [**Ayoub Benaissa**](https://github.com/youben11)


<table>
  <tr>
    <td align="center">
      <a href="https://github.com/youben11">
        <img src="https://avatars0.githubusercontent.com/u/21220087?s=240" width="170px;" alt="">
        <br /><sub><b>Ayoub Benaissa</b></sub></a><br />
        <sub>CrypTen + TenSEAL</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/philomath213">
        <img src="https://avatars3.githubusercontent.com/u/20177422?s=460" width="170px;" alt="">
        <br /><sub><b>Bilal Retiat</b></sub></a><br />
        <sub>TenSEAL</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/IamRavikantSingh">
        <img src="https://avatars2.githubusercontent.com/u/40258150?s=460&v=4" width="170px;" alt="">
        <br /><sub><b>Ravikant Singh</b></sub></a><br />
        <sub>BFV scheme (PySyft)</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/bcebere">
        <img src="https://avatars0.githubusercontent.com/u/1623754?s=460&v=4" width="170px;" alt="">
        <br /><sub><b>Bogdan Cebere</b></sub></a><br />
        <sub>Homomorphic Encryption</sub>
        <sub>TenSEAL</sub>
      </a>
    </td>  

  </tr>
</table>


### [Functional Encryption](./fe)

This team is led by [**S P Sharan**](https://github.com/Syzygianinfern0)

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/Syzygianinfern0">
        <img src="https://avatars2.githubusercontent.com/u/31875325?s=460" width="170px;" alt="">
        <br /><sub><b>S P Sharan</b></sub></a><br />
        <sub>Core dev in SMPC</sub>
      </a>
    </td>
  </tr>
</table>


### [Private Set Intersection](./psi)

This team is led by [**Michael Höh**](https://www.linkedin.com/in/michael-hoeh/)

<table>
  <tr>
    <td align="center">
      <a href="https://www.linkedin.com/in/michael-hoeh/">
        <img src="https://media-exp1.licdn.com/dms/image/C4D03AQE_K_Ga31Mekg/profile-displayphoto-shrink_200_200/0?e=1602720000&v=beta&t=Ehev1hXvGRyeLYtdhFmQ5xBHg7pD-aJiE-w3GcpVbAI" width="170px;" alt="">
        <br /><sub><b>Michael Höh</b></sub></a><br />
        <sub>PSI Team Lead</sub>
      </a>
  </tr>
</table>


## Weekly Meetings

We have weekly meetings that are currently private, [but we take detailed notes for each meeting](./meetings). Here you can will find our weekly status updates: where each member of our team has recorded what they worked on the previous week and what they plan to work on in the upcoming week.

## Contact

### Want to join?

If you are interested to to work on cryptography related use cases, you should definitely join us!

*[Apply to the cryptography team!](https://forms.gle/BWmYQJrCwqe1m3ex5)*

### Have questions?

Reach us on [Slack](http://slack.openmined.org/)!

Or on Twitter: [**@theoryffel**](https://twitter.com/theoryffel) [**@y0uben11**](https://twitter.com/y0uben11) [**@GeorgeMuraru**](https://twitter.com/GeorgeMuraru) [**@michaelhoeh**](https://twitter.com/michaelhoeh) 
