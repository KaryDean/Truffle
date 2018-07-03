# RUNNING MIGRATIONS运行转移

## [原网址](https://truffleframework.com/docs/getting_started/migrations)

> Migrations are JavaScript files that help you deploy contracts to the Ethereum network. 
> These files are responsible for **staging** your deployment tasks, 
> and they're written under the assumption that your deployment needs will change over time.

这里指出Migrations是JavaScript文件，帮助你部署合约到以太坊网络中
这些文件用来负责你的部署任务的分层工作。staging的意思应该和第一篇的意思差不多，是按照前缀的顺序执行的。
执行代码是：
`$ truffle migrate`

> This will run all migrations located within your project's migrations directory. At their simplest, migrations are simply a > set of managed deployment scripts. If your migrations were previously run successfully, truffle migrate will start execution > from the last migration that was ran, running only newly created migrations. If no new migrations exists, truffle migrate > > won't perform any action at all. You can use the --reset option to run all your migrations from the beginning. For local > > > testing make sure to have a test blockchain such as Ganache installed and running before executing migrate.

和之前编译一样，只会部署你改变的内容。如果想要全部重新部署，就添加`--reset`关键词。同时要保证运行时有一个测试区块链可以用于迁移

类似代码：4_example_migration.js
```
var MyContract = artifacts.require("MyContract");

module.exports = function(deployer) {
  // deployment steps
  deployer.deploy(MyContract);
};
```
> Note that the filename is prefixed with a number and is suffixed by a description.
为了记录迁移是否成功，需要使用编号的前缀。后缀纯粹是为了人类的可读性和理解力。

第一行代码`artifacts.require("MyContract");`表示我们想要与那些代码交互
还是选择之前的平台吧，这是实在不方便
# [感想](http://bbfdb076.wiz03.com/share/s/2X_r1S09nA3z2p2way2DKAAg3LQ9oh1-3QIP2ONRSp3h-u-1)
