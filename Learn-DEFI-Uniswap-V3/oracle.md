# Uniswap V3
## 预言机介绍

https://liaoph.com/uniswap-v3-5/

调用指定交易对pool合约的observe函数即可

```
const Web3 = require('web3');
const contractFile = require('./eth-usdt.json') //交易对pool合约abi

const web3 = new Web3(new Web3.providers.HttpProvider('https://mainnet.infura.io/v3/ea105d55c4394f4fb7b58d29c877e797'));
address = "0x8ad599c3A0ff1De082011EFDDc58f1908eb6e6D8";
const first_time = 1;
const second_time = 10;

const contract = new web3.eth.Contract(contractFile,address)
const get_price = async() => {
    ticks = await contract.methods.observe([first_time,second_time]).call()

    console.log(ticks);
    tick_price = (ticks['tickCumulatives'][0] - ticks['tickCumulatives'][1])/(second_time - first_time)
    eth_price = Math.pow(10,12)/Math.pow(1.0001,tick_price)
    console.log(eth_price);
   };

get_price();

```
