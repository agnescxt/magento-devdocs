---
group: install_cli
subgroup: 05_Command-line installation
title: 启用或禁用模块
menu_title: 启用或禁用模块
menu_node:
menu_order: 7
version: 2.0
github_link: install-gde/install/cli/install-cli-subcommands-enable.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-subcommands-enable.html
  - /guides/v2.0/install-gde/install/install-cli-subcommands-enable.html
functional_areas:
  - Install
  - System
  - Setup
---


<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

<h2 id="instgde-cli-subcommands-enable-disable-prereq">先决条件</h2>
此命令没有前提条件

<h2 id="instgde-cli-subcommands-enable-disable">模块的启用,禁用</h2>
要启用或禁用模块，请使用下面的命令：

	magento module:enable [-c|--clear-static-content] [-f|--force] [--all] <module-list>
	magento module:disable [-c|--clear-static-content] [-f|--force] [--all] <module-list>

where

*	`<module-list>` 是一个你要启用或禁用的以空格分开的模块列表。如果任何{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}名字包含特殊字符，请用单引号或双引号引起来。
*	`--all`来同时启用或禁用所有的模块
*	`-f`或`--force` 来强制一个启用或禁用一个模块不管是否有依赖。在使用这个选项前，请参考<a href="#instgde-cli-subcommands-enable-modules">关于启用和禁用模块</a>.
*	`-c`或`--clear-static-content` 来清除<a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html#config-cli-static-overview">生成的静态视图文件</a>.

	如果有多个同名文件并且你没有全部清除它们，清除静态视图文件可以导致失败。

	换句话说，因为<a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">静态文件归并</a>规则, 如果你没有清除静名字都是`logo.gif`的不同文件，归并可能导致错误的文件被展示。

使用下面的命令来列出所有启用或未启用的模块：

	magento module:status

例如，要禁用Weee模块，执行：

	magento module:disable Magento_Weee

更多关于启用和禁用模块的信息请参考<a href="#instgde-cli-subcommands-enable-modules">关于启用和禁用模块</a>.

<h2 id="instgde-cli-subcommands-enable-update">更新数据库</h2>
如果你启用了一个或多个模块，使用下面的命令来更新数据库：

	magento setup:upgrade

<h2 id="instgde-cli-subcommands-enable-modules">关于启用和禁用模块</h2>
{% include install/enable-disable-modules.html %}

#### 相关主题

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">使用命令行安装Magento</a>
*	[移除样本数据模块或更新样本数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-sample-data-other.html)
*	[启用或禁用模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html)
*	[显示或更改管理面板的URI]({{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html)
*	[卸载模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">建立或更新布署配置</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-maint.html">开启或关闭维护模式</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html">创建Magento的数据库表结构</a>
*	[更新数据库表结构和数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db-upgr.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-store.html">配置网店</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-admin.html">创建或解锁Magento管理员</a>
*	[备份和还原文件系统，媒体文件和数据库]({{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html)
*	[卸载主题]({{ page.baseurl }}/install-gde/install/cli/install-cli-theme-uninstall.html)
*	[卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>
