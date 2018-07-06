# NPM的包管理
Truffle 符合NPM标准。你的项目中有一个*node_modules*文件夹。这意味着你可以使用和分发合约，dapps还有以太坊支持的库通过NPM，让你自己的代码可以位别人所用，也可以用别人的代码。

## 包布局
一般存放在两个文件夹中：
1. */contracts*
2. */build*其中包含由Truffle创建的*/build/contracts*。*/build/contracts*主要包含，由*/contracts*中原始的solidity代码生成的JSON文件

## 使用包
是用别人的包，主要用在两个地方，一个是自己的合约里*/contract*，第二个就是你的JS代码（迁移*/migrations*还有测试*/test*）
### 安装
这里举了一个例子：
```
$ cd my_project
$ npm install example-truffle-library
```

包的内容存放在*my_project/node_modules*文件夹中。
### 在自己的合约中导入包
`import "example-truffle-library/contracts/SimpleNameRegistry.sol";`
### 在JS代码中
```
var contract = require("truffle-contract");
var data = require("example-truffle-library/build/contracts/SimpleNameRegistry.json");
var SimpleNameRegistry = contract(data);
```
### 包部署的地址
如果你的合约想要与已经部署过得合约交互。这些已经部署过得合约的地址存放在包的*.json*文件中。让自己的合约接受来自需要依赖的合约的地址，然后使用migrations。
举个例子：
*MyContract.sol*
```
pragma solidity ^0.4.13;

import "example-truffle-library/contracts/SimpleNameRegistry.sol";

contract MyContract {
  SimpleNameRegistry registry;
  address public owner;

  function MyContract {
    owner = msg.sender;
  }

  // Simple example that uses the deployed registry from the package.
  function getModule(bytes32 name) returns (address) {
    return registry.names(name);
  }

  // Set the registry if you're the owner.
  function setRegistry(address addr) {
    require(msg.sender == owner);

    registry = SimpleNameRegistry(addr);
  }
}
```
*3_hook_up_example_library.js*
```
// Note that artifacts.require takes care of creating an abstraction for us.
var SimpleNameRegistry = artifacts.require("example-truffle-library/SimpleNameRegistry");

module.exports = function(deployer) {
  // Deploy our contract, then set the address of the registry.
  deployer.deploy(MyContract).then(function() {
    return MyContract.deployed();
  }).then(function(deployed) {
    return deployed.setRegistry(SimpleNameRegistry.address);
  });
};
```
## 发布之前
在发布你自己的包之前，考虑使用下面的指令移除多余的网络人工制造物。
`$ truffle networks --clean`
