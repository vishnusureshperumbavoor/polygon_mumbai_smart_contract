# Smart Contract Deployment
Deployment of a hello world smart contract into Polygon Mumbai testnetwork using Hardhat, MetaMask and Alchemy.

## Polygon mumbai explorer
You can see the transaction details at [https://mumbai.polygonscan.com/address/0xdaDE9f41f5FaD4B1CEc949AA6D3630dd3FE0Be54?s=08](https://mumbai.polygonscan.com/address/0xdaDE9f41f5FaD4B1CEc949AA6D3630dd3FE0Be54?s=08)

## Prerequisits
1. NodeJS and VSCode
2. [MetaMask](https://metamask.io/download/) should be installed on your chrome browser
3. Create new app on [alchemy](https://dashboard.alchemy.com/apps) and get the API key
   
## Getting Started
Clone the repository
```
git clone https://github.com/vishnusureshperumbavoor/polygon_mumbai_smart_contract.git
```
Open VSCode
```
code polygon_mumbai_smart_contract
```
Globally install hardhat (if it doesn't exist)
```
npm install --save-dev hardhat
```
Install necessary dependecides
```
npm i
```
Provide your alchemy API key and metamask private key in the [.env](.env) file
```
API_URL = "https://polygon-mumbai.g.alchemy.com/v2/your-api-key"
PRIVATE_KEY = "your-metamask-private-key"
```
Compile the smart contracts
```
npx hardhat compile
```
Deploy the smart contracts
```
npx hardhat run scripts/deploy.js --network polygon_mumbai
```
Expected output
```
Contract deployed to address: 0x3d94af870ED272Cd5370e4135F9B2Bd0e311d65D
```
Go to the [polygon mumbai explorer](https://mumbai.polygonscan.com/) and search for the output you got.

# How to create an application like this
Initialize your project
  ```sh
  mkdir hello-world
  cd hello-world
  ```
Installation
   ```sh
   npm init -y
   ```
Install Hardhat
  ```sh
  npm install --save-dev hardhat
  ```
Create Hardhat project
```sh
npx hardhat
```
Add project folders
```sh
mkdir contracts
mkdir scripts
```
Navigate to contracts folder
```
cd contracts
```
Create a file called Helloworld.sol and type
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
Install the dotenv package
```sh
npm install dotenv --save
```
Add alchemy app API key and metamask private key to the .env
```sh
API_URL = "https://polygon-mumbai.g.alchemy.com/v2/your-api-key"
PRIVATE_KEY = "your-metamask-private-key"
```
Install ethers.js
```sh
npm install --save-dev @nomiclabs/hardhat-ethers "ethers@^5.0.0"
```
Update hardhat.config.js
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
Compile the smart contract
```sh
npx hardhat compile
```
Navigate to scripts folder
```
cd ..
cd scripts
```
Create a file called deploy.js & write the code
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
Deploy your smart contracts
```sh
npx hardhat run scripts/deploy.js --network polygon_mumbai
```
You should see something like this:
```sh
Contract deployed to address: 0x3d94af870ED272Cd5370e4135F9B2Bd0e311d65D
```
Go to the [polygon mumbai explorer](https://mumbai.polygonscan.com/) and search for the output you got.
## Contact
Contact
For any inquiries or feedback, please contact [Vishnu Suresh Perumbavoor](https://vishnusureshperumbavoor.github.io/V-S-P/) at <br> <br>
[![LinkedIn][linkedin-shield]][linkedin-url]
[![github][github-shield]][github-url]
[![Twitter][twitter-shield]][twitter-url]
[![Linktree][linktree-shield]][linktree-url]
[![Instagram][instagram-shield]][instagram-url]
[![GMail][gmail-shield]][gmail-url]


## Contributions
It is open for contributions. Anyone can clone it and create pull request

[linkedin-shield]: https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white
[linkedin-url]: https://www.linkedin.com/in/vishnu-suresh-perumbavoor/
[twitter-shield]: https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white
[twitter-url]: https://twitter.com/in/vspeeeeee
[instagram-shield]: https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white
[instagram-url]: https://www.instagram.com/vishnusureshperumbavoor/
[linktree-shield]: https://img.shields.io/badge/linktree-39E09B?style=for-the-badge&logo=linktree&logoColor=white
[linktree-url]: https://linktr.ee/vishnusureshperumbavoor2.0
[github-shield]: https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white
[github-url]: https://github.com/vishnusureshperumbavoor
[gmail-shield]: https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white
[gmail-url]: mailto:vishnusureshperumbavoor@gmail.com

