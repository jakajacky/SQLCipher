# SQLCipher
SQLCipher数据库加密配置说明

<!DOCTYPE html>
<html>
<body>
<div style="width: 1200px;">
	<br>
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
<br>
	<h2 style="color: #146a94;">Xcode项目配置</h2>
	<p style="line-height: 25px;">将SQLCipher库提供<font color="#c7254e">sqlcipher.xcodeproj</font>文件添加到你的项目中，编译成静态库，并链接到项目target上。</p>
	<h3 style="color: #146a94;">添加项目依赖</h3>
	<p style="line-height: 25px;">在Xcode中打开您的iOS应用程序的项目或工作区，在左侧文件目录中找到iOS应用程序的顶级Project图标并单击选中。右键单击该处，然后选择<font color="#146a94">“Add Files to 'XXX'”</font>（XXX将根据您的应用程序的名称而有所不同）。由于我们将SQLCipher直接克隆到与iOS应用程序相同的文件夹中，所以您应该在根项目文件夹中看到一个<font color="#c7254e">sqlcipher</font>文件夹。打开此文件夹并选择<font color="#c7254e">sqlcipher.xcodeproj</font>:</p>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/add-sqlcipher-project-file.png"></img>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/select-sqlcipher-project-file.png"></img>
<br>
	<h3 style="color: #146a94;">添加Project配置项</h3>
	<p style="line-height: 25px;">开始设置Project的Build settings（注意是Project，而不是Targets），选中Build Settings，搜索“Header Search Paths”，对应的增加路径：<font color="#c7254e">$(PROJECT_DIR)/sqlcipher</font>:</p>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/tech.png"></img>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/sqlcipher-xcode-header-search-paths.png"></img>
	<p style="line-height: 25px;">接下来，搜索“Other Linker Flags”，对应的增加路径：<font color="#c7254e">$(BUILT_PRODUCTS_DIR)/libsqlcipher.a</font>，并拖动放到第一个位置，以确保SQLCipher是第一个被链入你的项目的静态库</p>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/sqlcipher-xcode-other-linker-flags.png"></img>
	<p style="line-height: 25px;">然后，搜索“Other C Flags”，对应的增加路径：<font color="#c7254e">-DSQLITE_HAS_CODEC</font>，确保SQLCipher能够编译成功</p>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/sqlcipher-xcode-other-c-flags.png"></img>
<br>
	<h3 style="color: #146a94;">添加Targets配置项</h3>
	<p style="line-height: 25px;">下一步，选择“Targets”，给项目的target增加Target依赖确保SQLCipher在项目代码前面编译，选择”Build phases“</p>
	<p style="line-height: 25px;">展开”Target Dependencies“，点击<font color="#c7254e">+</font>在文件中选择<font color="#c7254e">sqlcipher</font>静态库：</p>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/sqlcipher-xcode-select-target-dependency.png"></img>
	<p style="line-height: 25px;">展开”Link Binary With Libraries“，点击<font color="#c7254e">+</font>在文件中选择<font color="#c7254e">libsqlcipher.a</font>静态库：</p>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/sqlcipher-xcode-link-binary-with-libraries.png"></img>
	<p style="line-height: 25px;">最后，再给”Link Binary With Libraries“添加”Security.framework“。</p>
	<img src="https://github.com/jakajacky/SQLCipher/blob/master/img/sqlcipher-add-security-framework.png"></img>
	<p style="line-height: 25px;color: #146a94">Tip:如果libsqlite3.dylib或者其他SQLite库已经存在于”Link Binary With Libraries“列表中，记得要删除掉！！！</p>

</div>
</body>
</html>
