# Truffle
## 初始化一个项目Quickstart![https://truffleframework.com/docs/getting_started/project]（https://truffleframework.com/docs/getting_started/project）

现有项目：You can use the truffle unbox <box-name> command to download any of the other Truffle Boxes.

空项目：To create a bare Truffle project with no smart contracts included, use truffle init.

用来管理和更新你部署的智能合约的状态[Migrations.sol]Open the contracts/Migrations.sol file. This is a separate Solidity file that manages and updates the status of your deployed smart contract. This file comes with every Truffle project, and is usually not edited.


Open the migrations/1_initial_deployment.js file. This file is the migration (deployment) script for the Migrations contract found in the Migrations.sol file.用来给Migrations.sol做迁移用的脚本

Open the migrations/2_deploy_contracts.js file. This file is the migration script for the MetaCoin contract. (Migration scripts are run in order, so the file beginning with 2 will be run after the file beginning with 1.)这个是给MetaCoin智能合约迁移的脚本，迁移脚本是按顺序执行的，2会跟在1后面执行


Open the truffle.js file. This is the Truffle configuration file, for setting network information and other project-related settings. The file is blank, but this is okay, as we'll be using a Truffle command that has some defaults built-in.Truffle.js是truffle配置文件，设置网络信息和其他项目相关的设定。
pragma solidity ^0.4.2;
​
import "truffle/Assert.sol";
import "truffle/DeployedAddresses.sol";
import "../contracts/MetaCoin.sol";
​
contract TestMetacoin {
​
  function testInitialBalanceUsingDeployedContract() public {
    MetaCoin meta = MetaCoin(DeployedAddresses.MetaCoin());//使用一个已经部署好的合约定义一个对象
    //定义一个合约MetaCoin对象meta
​
    uint expected = 10000;
​
    Assert.equal(meta.getBalance(tx.origin), expected, "Owner should have 10000 MetaCoin initially");
    //判断是不是相等
  }
​
  function testInitialBalanceWithNewMetaCoin() public {
    MetaCoin meta = new MetaCoin();//使用一个新的合约定义一个对象
​
    uint expected = 10000;
​
    Assert.equal(meta.getBalance(tx.origin), expected, "Owner should have 10000 MetaCoin initially");
  }
​
}
​
编译：Compile the smart contracts:

truffle compile


You can create this blockchain and interact with it using Truffle Develop.//使用
truffle develop
创建一个个人链用于测试
On the Truffle Develop prompt, Truffle commands can be run by omitting the truffle prefix. For example, to run truffle compile on the prompt, type compile. The command to deploy your compiled contracts to the blockchain is truffle migrate, so at the prompt, type:
在有Truffle Develop提示符的地方可以忽略truffle前缀。
执行truffle develop结果
Truffle Develop started at http://127.0.0.1:9545/
​
Accounts:
(0) 0x627306090abab3a6e1400e9345bc60c78a8bef57
(1) 0xf17f52151ebef6c7334fad080c5704d77216b732
(2) 0xc5fdf4076b8f3a5357c5e395ab970b5b54098fef
(3) 0x821aea9a577a9b44299b9c15c88cf3087f3b5544
(4) 0x0d1d4e623d10f9fba5db95830f7d3839406c6af2
(5) 0x2932b7a2355d6fecc4b5c0b6bd44cc31df247a2e
(6) 0x2191ef87e392377ec08e7c08eb105ef5448eced5
(7) 0x0f4f2ac550a1b4e2280d04c21cea7ebd822934b5
(8) 0x6330a553fc93768f612722bb8c2ec78ac90b3bbc
(9) 0x5aeda56215b167893e80b4fe645ba6d5bab767de
​
Private Keys:
(0) c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3
(1) ae6ae8e5ccbfb04590405997ee2d52d2b330726137b875053c36d94e974d162f
(2) 0dbbe8e4ae425a6d2687f1a7e3ba17bc98c673636790f1b8ad91193c05875ef1
(3) c88b703fb08cbea894b6aeff5a544fb92e78a18e19814cd85da83b71f772aa6c
(4) 388c684f0ba1ef5017716adb5d21a053ea8e90277d0868337519f97bede61418
(5) 659cbb0e2411a44db63778987b1e22153c086a95eb6b18bdf89de078917abc63
(6) 82d052c865f5763aad42add438569276c00d3d88a2d062d36b2bae914d58b8c8
(7) aa3680d5d48a8283413f7a108367c7299ca73f553735860a87b08f39395618b7
(8) 0f62d96d6675f32685bbdb8ac13cda7c23436f63efbb9d07700d8669ff12b7c4
(9) 8d5366123cb560bb606379f90a0bfd4769eecc0557f1b362dcae9012b548b1e5
​
Mnemonic: candy maple cake sugar pudding cream honey rich smooth crumble sweet treat
​
⚠️  Important ⚠️  : This mnemonic was created for you by Truffle. It is not secure.
Ensure you do not use it on production blockchains, or else you risk losing funds.   
​
truffle(development)>
将编译好的智能合约部署到区块链上The command to deploy your compiled contracts to the blockchain is truffle migrate, so at the prompt, type:部署结果：
Using network 'develop'.
​
Running migration: 1_initial_migration.js//先执行1_initial_migration.js脚本
  Deploying Migrations...//部署
  ... 0x63b393bd50251ec5aa3e159070609ee7c61da55531ff5dea5b869e762263cb90
  Migrations: 0x8cdaf0cd259887258bc13a92c0a6da92698644c0
Saving successful migration to network...//成功部署
  ... 0xd7bc86d31bee32fa3988f1c1eabce403a1b5d570340a3a9cdba53a472ee8c956
Saving artifacts...//保留人工产品artifacts是一个特定的标识符
Running migration: 2_deploy_contracts.js//在执行 2_deploy_contracts.js脚本
  Deploying ConvertLib...
  ... 0xa59221bc26a24f1a2ee7838c36abdf3231a2954b96d28dd7def7b98bbb8a7f35
  ConvertLib: 0x345ca3e014aaf5dca488057592ee47305d9b3e10
  Linking ConvertLib to MetaCoin
  Deploying MetaCoin...
  ... 0x1cd9e2a790f4795fa40205ef58dbb061065ca235bee8979a705814f1bc141fd5
  MetaCoin: 0xf25186b5081ff5ce73482ad761db0eb0d25abfbf
Saving successful migration to network...
  ... 0x059cf1bbc372b9348ce487de910358801bbbd1c89182853439bec0afaee6c7db
Saving artifacts...
这是2_deploy_contracts.js代码，可以从中看见与之对应的操作。
1、2两行表示需要这两个智能合约
正文操作：
deployer.deploy(ConvertLib);因为要调用ConvertLib所以，先部署
deployer.link(ConvertLib, MetaCoin);再将这两者连接起来，估计是因为MetaCoin合约的部署要用到ConvertLib的哈希地址，用于调用
deployer.deploy(MetaCoin);最后部署MetaCoin
var ConvertLib = artifacts.require("./ConvertLib.sol");
var MetaCoin = artifacts.require("./MetaCoin.sol");
​
module.exports = function(deployer) {
  deployer.deploy(ConvertLib);
  deployer.link(ConvertLib, MetaCoin);
  deployer.deploy(MetaCoin);
};
​
查看部署MetaCoin的账户有多少余额
MetaCoin.deployed().then(function(instance){return instance.getBalance(web3.eth.accounts[0]);}).then(function(value){return value.toNumber()});
查看余额值多少以太币
MetaCoin.deployed().then(function(instance){return instance.getBalanceInEth(web3.eth.accounts[0]);}).then(function(value){return value.toNumber()});
这种语言的书写方式大概为
首先从部署的合约中虚拟出一个对象，MetaCoin.deployed( )这样新建出一个实例instance用于下一步
然后是.then(function(instance){return instance.getBalanceInEth(web3.eth.accounts[0])})，上一步的合约实例对象instance，我们可以用来调用内部函数getBalanceInEth，内部输入变量为第一个地址，也就是初始化这个合约的地址，返回的是一个余额对象
return balances[addr];
，也就是20000，因为这一步获得是一个余额对象，操作起来不方便，需要将它转化为数值，最后一步用来将它转化为数值
最后是.then(function(value){return value.toNumber()})上一步返回的对象赋值给value，value执行特定的函数toNumber()转化为数值
这里的赋值的新变量应该是直接临时定义出来的，固定结构，function(value)中的value就是上一个函数return的结果
获取转账之后另一个账户的余额
MetaCoin.deployed().then(function(instance1){return instance1.getBalance(web3.eth.accounts[1]);}).then(function(value){return value.toNumber();});//自己编写的函数
