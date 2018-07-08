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
