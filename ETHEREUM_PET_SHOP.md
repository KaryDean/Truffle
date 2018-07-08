# ETHEREUM PET SHOP
[原文地址](https://truffleframework.com/tutorials/pet-shop)
这里只是自己的一些笔记，文中提到一些知识作为自己的笔记

1. 数组包含一种类型可以是*定长*也可以是*变长*
2. Public这个变量会自动有一个getter方法，需要一个关键字，每次仅返回一个值。
3. 函数参数及返回值一定要制定。
4. 
> * The address of the person or smart contract who called this function is denoted by msg.sender * 
这里提到了一句话，调用这个函数的*人或者智能合约*的地址被称为msg.sender.
5. Solidity 是一个编译语言，意味着我们需要将我们Solidity编译为以太坊虚拟机（EVM）可读的字节码，然后让虚拟机可以执行。
所以顺序是先编译，再部署。
现有compile，再有migration
6. Adoption adoption = Adoption(DeployedAddressed.Adoption());利用这种方法获取，应该是后面一个DeployedAddressed这个方法获取地址。
7. 应用接口application binary interface（ABI）定义了如何与合约交互的对象，其中包括变量、函数和他们的参数。
8. 初始化web3，设置一个提供者。set a provider：
```[官网](https://github.com/ethereum/web3.js/)
if (typeof web3 !== 'undefined') {
  web3 = new Web3(web3.currentProvider);
} else {
  // set the provider you want from Web3.providers
  web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
}
```
```[petshop网](https://truffleframework.com/tutorials/pet-shop)
// Is there an injected web3 instance?
if (typeof web3 !== 'undefined') {
  App.web3Provider = web3.currentProvider;
} else {
  // If no injected web3 instance is detected, fall back to Ganache
  App.web3Provider = new Web3.providers.HttpProvider('http://localhost:7545');
}
web3 = new Web3(App.web3Provider);
```
解析：这里的第一个if语句中结果是一致的，这里的App.web3Provider是App里的一个变量。
然后petshop中将else中的结果分为两部，如果检测到web3实例，那么就新建一个自己的实例，使用Ganache。这里只是对于web3Provider而已。接着在外面就开始新建这个web3了。
