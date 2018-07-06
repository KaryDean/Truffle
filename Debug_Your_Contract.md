# 给你的合约找Bug
## 初览
在区块链上调试事务时，您没有实时运行代码; 相反，您将逐步执行该事务的历史执行，并将该执行映射到其关联的代码上。（直接翻译来的）。它给我们提供了很多debug工具。
为了debug交互需要以下几种东西：
1. Truffle4.0或者更高版本
2. 交易的哈希值
3. 源代码还有交易遇到的工件。原文是：
> artifacts the transaction encounters.
# 感觉直接使用在线编辑工具也可以达到这种效果[连接地址]([Remix - Solidity IDE](https://remix.ethereum.org/#optimize=true&version=soljson-v0.4.16+commit.d7661dd9.js))
