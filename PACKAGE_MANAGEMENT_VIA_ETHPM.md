# PACKAGE MANAGEMENT VIA ETHPM
- 发现使用Bear，编辑markdown格外简单，还免费，不是广告

[原文地址](https://truffleframework.com/docs/getting_started/packages-ethpm#package-configuration)
> EthPM is the new Package Registry for Ethereum. It follows the ERC190 spec for publishing and consuming smart contract packages, and has gained wide support from many diverse Ethereum development tools.

EthPM就是类似于NPM的包登记库。用来存放以太坊包。
安装方法：
`$ truffle install <package name>`
`$ truffle install <package name>@<version>`
[这个网址可以用来查找这些包]([The Ethereum Package Registry](https://www.ethpm.com/registry))

## CONSUMING INSTALLED CONTRACTS
使用这些合约
你安装的合约都在*installed_contracts*文件夹里 ,NPM安装的文件都在*node_modules*文件夹里。

可以使用`import`或者`require`调用这些合约
*.sol文件*
```
pragma solidity ^0.4.2;

import "owned/owned.sol";

contract MyContract is owned {
  // ...
}
```
*./migrations/2_deploy_contracts.js文件*
```
var ENS = artifacts.require("ens/ENS");
var MyContract = artifacts.require("MyContract");

module.exports = function(deployer) {
  // Only deploy ENS if there's not already an address already.
  // i.e., don't deploy if we're using the canonical ENS address,
  // but do deploy it if we're on a test network and ENS doesn't exist.
  deployer.deploy(ENS, {overwrite: false}).then(function() {
    return deployer.deploy(MyContract, ENS.address);
  });
};
```
> Note that in the migration above, we consume the ens package and deploy the ENS contract conditionally based on whether or not ENS already has an address set. This is a fancy trick provided to you by the deployer that makes it much easier to write migrations dependent on the the existence of network artifacts. 

我们使用了ens包，但是我们可以根据情景选择部署还是不部署。如果已经部署了就不需要部署了。比如在Ropsten网络中，就不需要部署了，因为已经有人部署过了，直接调用就行了。

## 发布自己的合约
原文中也提到了如果发布自己的合约，这里就不提了。
