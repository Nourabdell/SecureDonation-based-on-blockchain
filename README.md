# SecureDonation-based-on-blockchain
Secure Donation Project  based on truffle /metamask/ganache  Your guide to build a project donation based on blockchain in order to ensure the traceability and the security of your money donation. Steps :  Step 1:Setup your IDE coding in my case i choose VS code  1-I install  the extension of truffle on VS Code .and I learn the basics of truffle thanks to the official site : https://trufflesuite.com/docs/truffle/   by the way truffle is just a development environment to code and compile your smart contract and is testing framework for blockchains using the ethereum virtual machine .So let’s take the first step : I created a folder named Nour project using this command : mkdir NourProject and also inside it i created 2 other folders  :mkdir frontend and mkdir Blockchain   Step2:Start with truffle  so now let’s create our truffle project inside Nourproject/Blockchain thanks to the command truffle init   Now let’s create our smart contract named Donation.sol in Nourproject/Blockchain/contracts  and in direction Nourproject/Blockchain/migration/Donation.js fo deploying later your smart contract on ganache we will use this fil!e .js   So our smart Contract looks like: //SPDX-License-Identifier:MIT pragma solidity ^0.8.0; //so contract Donation{    //struct :define your type Donor    //inside struct you can grouping your different information that you wanna track it    struct Donor{        //uint (only integer without minus)        uint id ;//id of donor        string name;// the name of donor        uint256 amount;// the amount of donor        address sender_address;//Donprs wallet address    }    uint256 id=0;    //Mapping is Mapping is a reference type as arrays and structs as dictionnary in python is composed essentially by key =>value    mapping(uint=>Donor)public sender;    //function to add another donor to take a place    //payble is function its role to recieve ETH from donors in oder to store    //donors data and the amount paid    function addDonor(string memory name)public payable {        id+=1;        sender[id]=Donor(id,name,msg.value,msg.sender);    }    So now let’s how to complelete the donation.js in migration   so after coding our smart contract we have install ganache thanks to this link: https://trufflesuite.com/ganache/ so now let’s compile the smart contract thans to this command truffle compile   before we deploy it into ganache we have to add the project into ganache     now let’s relate ganache to truffle test    so let’s deploy it into the ganache (local blockchain test ): truffle migrate    Step3 :Frontend part  this part based on html /css/js  So in this part just we use the basic tools of html/css/js  as u see here in the  image bellow :  so let’s understand some buttons function as the button connect  this button it’s main function is to extract address account from metamask  so the steps that you should follow it in this part just build a simple button thanks to bootstrap  https://getbootstrap.com/docs/5.2/getting-started/introduction/ and create a simple squelette of form  and add some animation thanks to css  so let’s add the script of  web3.js to let our website worked on blockchain browser thanks to this script  &lt;script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js">&lt;/script> so enable it by writing this piece of code  //Enable Web3 async function loadWeb3(){    if(window.ethereum) {        window.web3 = new Web3(window.ethereum);    } }  and then load smart contract from truffle thanks to it’s ABI and it’s address : you can find the ABI in build file it will create automatic when you built your contract  so in my case my ABI is located in the direction of build /Donation.json   so My ABI : "abi": [    {      "inputs": [        {          "internalType": "uint256",          "name": "",          "type": "uint256"        }      ],      "name": "sender",      "outputs": [        {          "internalType": "uint256",          "name": "id",          "type": "uint256"        },        {          "internalType": "string",          "name": "name",          "type": "string"        },        {          "internalType": "uint256",          "name": "amount",          "type": "uint256"        },        {          "internalType": "address",          "name": "sender_address",          "type": "address"        }      ],      "stateMutability": "view",      "type": "function"    },    {      "inputs": [        {          "internalType": "string",          "name": "name",          "type": "string"        }      ],      "name": "addDonor",      "outputs": [],      "stateMutability": "payable",      "type": "function"    }  ], So the address is the same of the contract address :  so after loading the smart contract thanks to it’s ABI and address you can read data from and load all of it’s function by some code in js and then connect to the metamask wallet and get the address of the account after just donate by the button donate   all of :this detail is written in code js you can say it in code js in the code file    wish that document is helpful   So as you see   after donate to ether thanks for some fake ethers in the metamask wallet which is take it fro the ganache balances  with simple steps just open metmask extension>settings >add network>then add the url rpc of your ganache  and in the id chain write 1337 after passing the transaction another block added in the ganache  so that’s all wish this documentation was helpful to you to understand the code how it running 