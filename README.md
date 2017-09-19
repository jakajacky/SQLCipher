# SQLCipher
SQLCipher数据库加密配置说明

<!DOCTYPE html>
<html>
<body>
<div style="width: 1200px;">
	<h1 style="color: #146a94;">为Xcode项目添加SQLCipher</h1>
	<p style="line-height: 25px;">SQLite已经是iOS应用程序中持久数据存储的流行API，因此开发的上升是显而易见的。作为一名程序员，您可以使用一个稳定的，经过充分记录的API，它可以在Objective-C中提供许多好的包装器，如FMDB和加密核心数据。所有安全问题都与应用程序代码完全脱钩，并由底层框架进行管理。
	<p style="line-height: 25px;">SQLCipher项目的框架代码是开源的，因此用户可以确信应用程序不使用不安全或专有的安全代码。此外，SQLCipher还可以在Android，Linux，OSX和Windows上编译，用于开发跨平台应用程序的用户。</p>
	<p style="line-height: 25px;">在iOS应用程序中使用SQLCipher是非常简单的。本文档描述了使用CommunityEdition源代码构建过程将SQLCipher集成到现有的iOS项目中。本教程假定您熟悉基本的iOS应用程序开发和Xcode（6.1.1）的工作安装。同样的基本步骤也可以应用于OSX项目。</p>
	<h2 style="color: #146a94;">准备工作</h2>
	<p style="line-height: 25px;">安装Xcode和iOS或者OSX SDK。访问<a style="color: #146a94;" href="https://developer.apple.com/xcode/">Apple Developer site</a>下载最新的Xcode和iOS、OSX SDKs</p>
	<h2 style="color: #146a94;">OpenSSL</h2>
	<p style="line-height: 25px;">OpenSSL已经不是在iOS或OSX上构建SQLCipher的必要步骤，因为该项目默认使用Apple的CommonCrypto框架进行硬件加速加密。如果您愿意，您仍然可以使用<a style="color: #146a94;" href="https://www.zetetic.net/blog/2013/6/27/sqlcipher-220-release.html">其他加密程序（如OpenSSL）构建SQLCipher</a>，或者您可以自己编写。</p>
	<h2 style="color: #146a94;">SQLCipher</h2>
	<p style="line-height: 25px;">启动终端，cd到你的项目根目录，使用git克隆SQLCipher代码</p>
	<pre><code>$ cd ~/Documents/code/SQLCipherApp
$ git clone https://github.com/sqlcipher/sqlcipher.git</code></pre>
</div>
</body>
</html>
