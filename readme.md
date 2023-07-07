<a name="readme-top"></a>
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h1 align="center">Smart Contract Deployment with Hardhat, Solidity, MetaMask, Polygon Mumbai Testnet, and Alchemy</h1>

  <p align="center">
    This project demonstrates the deployment of a smart contract using Hardhat, Solidity, MetaMask, the Polygon Mumbai Testnet, and Alchemy. The deployment process involves setting up the development environment, writing and testing the smart contract, and deploying it to the Polygon Mumbai Testnet.
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template">View Demo</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/issues">Report Bug</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/issues">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

### Technologies used

* Hardhat <br/>
A development environment for Ethereum that facilitates smart contract development, testing, and deployment.
* Solidty <br/>
A programming language for writing smart contracts on the Ethereum platform.
* Metamask <br/>
A browser extension wallet that allows interactions with Ethereum networks and decentralized applications.
* Polygon Mumbai Testnetwork <br/>
A test network provided by Polygon (previously Matic) for Ethereum-compatible smart contracts.
* Alchemy <br/>
A blockchain infrastructure provider that offers powerful APIs for interacting with Ethereum networks.

## Prerequisits
1. Install Node.js: <br>
Make sure you have Node.js installed on your machine. You can download it from the official Node.js website.

2. Install MetaMask:  <br>
Install the MetaMask extension for your browser and set up an account. Make sure you have some test Ether (MATIC) on the Polygon Mumbai Testnet.

3. Obtain Alchemy API Key: <br>
Sign up on the Alchemy website and obtain an API key. This key will be used to connect to the Polygon Mumbai Testnet.

<!-- GETTING STARTED -->
## Getting Started

This is an example of how you may give instructions on setting up your project locally.
To get a local copy up and running follow these simple example steps.

### Initialize your project

First, we’ll need to create a folder for our project. Navigate to your command line and type:
  ```sh
  mkdir hello-world
  cd hello-world
  ```

### Installation

Now that we’re inside our project folder, we’ll use npm init to initialize the project.

intialize node package manager
   ```sh
   npm init -y
   ```

### Install Hardhat

Hardhat is a development environment to compile, deploy, test, and debug your Ethereum software. 
Globally install hardhat if it doesn't exist
  ```sh
  npm install --save-dev hardhat
  ```

### Create Hardhat project
```sh
npx hardhat
```
generate an empty hardhat.config.js project

### Add project folders
Navigate to the root folder in the command line and type
```sh
mkdir contracts
mkdir scripts
```
* contracts/ is where we’ll keep our hello world smart contract code file
* scripts/ is where we’ll keep scripts to deploy and interact with our contract

### write the contract

1. navigate to the contracts folder and create Helloworld.sol
2. Copy and paste this code into your Helloworld.sol file
```sh
// SPDX-License-Identifier: None
pragma solidity >=0.8.9;
contract HelloWorld {
    event UpdatedMessages(string oldStr, string newStr);
    string public message;
    constructor(string memory initMessage) {
        message = initMessage;
    }
    function update(string memory newMessage) public {
        string memory oldMsg = message;
        message = newMessage;
        emit UpdatedMessages(oldMsg, newMessage);
    }
}
```

### Connect with metamask and Alchemy
Install the dotenv package in the root directory
```sh
npm install dotenv --save
```
Your .env should look like this:
```sh
API_URL = "https://polygon-mumbai.g.alchemy.com/v2/your-api-key"
PRIVATE_KEY = "your-metamask-private-key"
```

### Install ethers.js
```sh
npm install --save-dev @nomiclabs/hardhat-ethers "ethers@^5.0.0"
```

### Update hardhat.config.js
```sh
/**
* @type import('hardhat/config').HardhatUserConfig
*/

require('dotenv').config();
require("@nomiclabs/hardhat-ethers");

const { API_URL, PRIVATE_KEY } = process.env;

module.exports = {
   solidity: "0.8.9",
   defaultNetwork: "polygon_mumbai",
   networks: {
      hardhat: {},
      polygon_mumbai: {
         url: API_URL,
         accounts: [`0x${PRIVATE_KEY}`]
      }
   },
}
```

### compile the smart contract
```sh
npx hardhat compile
```
### write our deploy script
navigate to the scripts folder and create deploy.js
```sh
async function main() {
  const HelloWorld = await ethers.getContractFactory("HelloWorld");
  const hello_world = await HelloWorld.deploy("Hello World!");
  console.log("Contract deployed to address:", hello_world.address);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

### deploy your smart contracts
```sh
npx hardhat run scripts/deploy.js --network polygon_mumbai
```
You should see something like this:
```sh
Contract deployed to address: 0x3d94af870ED272Cd5370e4135F9B2Bd0e311d65D
```
Go to the [polygon mumbai explorer](https://mumbai.polygonscan.com/) and search for your smart contract

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request


<!-- CONTACT -->
## Contact

Vishnu Suresh Perumbavoor - [@vspeeeeee](https://twitter.com/vspeeeeee) - vishnusureshperumbavoor@gmail.com

## Additional Resources
* [Hardhat Documentation](https://hardhat.org/docs)
* [Solidity Documentation](https://docs.soliditylang.org/en/v0.8.20/)
* [MetaMask Documentation](https://docs.metamask.io/)
* [Polygon Mumbai Testnet Documentation](https://docs.polygonscan.com/v/mumbai-polygonscan/)
* [Alchemy Documentation](https://docs.alchemy.com/)

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/othneildrew/Best-README-Template/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png