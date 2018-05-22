---
group: install_cli
subgroup: 05_Command-line installation
title: Uninstall themes Composer packages
menu_title: Uninstall themes Composer packages
menu_node:
menu_order: 200
version: 2.0
github_link: install-gde/install/cli/install-cli-theme-uninstall.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-theme-uninstall.html
  - /guides/v2.0/install-gde/install/install-cli-theme-uninstall.html
functional_areas:
  - Install
  - System
  - Setup
---

<h2 id="instgde-install-uninst-theme-prereq">Prerequisite</h2>
Before you use this command, you must know the relative path to your theme. Themes are located in a subdirectory of `<your Magento install dir>/app/design/<area name>`. You must specify the path to the theme starting with the area, which is either `frontend` (for storefront themes) or `adminhtml` (for {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento Admin{% endglossarytooltip %} themes).

For example, the path to the Luma {% glossarytooltip d2093e4a-2b71-48a3-99b7-b32af7158019 %}theme{% endglossarytooltip %} provided with Magento 2 is `frontend/Magento/luma`.

For more information about themes, see <a href="{{ page.baseurl }}/frontend-dev-guide/themes/theme-structure.html">Magento theme structure</a>.

<h2 id="instgde-install-uninst-theme-over">Overview of uninstalling themes</h2>
This section discusses how to uninstall one or more themes, optionally including the themes' code from the file system. You can create backups first so you can restore the data at a later time.

This command uninstalls *only* themes that are specified in `composer.json`; in other words, themes that are provided as {% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %} packages. If your theme is not a Composer package, you must uninstall it manually by:

*	Updating the `parent` node information in `theme.xml` to remove references to the theme.
*	Removing theme code from the file system.

	<a href="{{ page.baseurl }}/frontend-dev-guide/themes/theme-inherit.html">More information about theme inheritance</a>.

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

<h2 id="instgde-install-uninst-theme-uninst">Uninstall themes</h2>
命令用法：

	magento theme:uninstall [--backup-code] [-c|--clear-static-content] {theme path} ... {theme path}

where

*	`{theme path}` is the relative path to the theme, starting with the area name. For example, the path to the Blank theme supplied with Magento 2 is `frontend/Magento/blank`.
*	`--backup-code` backs up the Magento 2 codebase as discussed in the paragraphs that follow.
*	`--clear-static-content` cleans generated <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html#config-cli-static-overview">static view files</a>, which is necessary to cause static view files to display properly.

此命令执行以下任务：

1.	Verifies that the specified theme paths exist; if not, the command terminates.
2.	Verifies that the theme is a Composer package; if not, the command terminates.
3.	Checks for dependencies; if there are any, the command terminates.

	To work around this, you can either uninstall all themes at the same time or you can uninstall the depending theme first.
4.	Verifies that the theme is not being used; if it is being used, the command terminates.
5.	Verifies that the theme is not the base of the virtual theme; if it is the base of a virtual theme, the command terminates.
6.	将网店设置为维护模式。
7.	If `--backup-code` is specified, backs up the Magento 2 codebase, excluding the `pub/static`, `pub/media`, and `var` directories.

	The backup file name is `var/backups/<timestamp>_filesystem.tgz`

	You can restore backups at any time using the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html#instgde-cli-uninst-mod-roll">magento setup:rollback</a> command.

8.	Removes themes from the `theme` database table.
9.	Remove themes from code base using `composer remove`.
10.	Cleans the {% glossarytooltip 0bc9c8bc-de1a-4a06-9c99-a89a29c30645 %}cache{% endglossarytooltip %}.
11.	Cleans generated classes
12.	If `--clear-static-content` is specified, cleans <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html#config-cli-static-overview">生成的静态视图文件</a>.

For example, if you attempt to uninstall a theme that another theme depends on, the following message displays:

	Cannot uninstall frontend/ExampleCorp/SampleModuleTheme because the following package(s) depend on it:
        ExampleCorp/sample-module-theme-depend

One alternative is to uninstall both themes at the same time as follows after backing up the Magento codebase:

	magento theme:uninstall frontend/ExampleCorp/SampleModuleTheme frontend/ExampleCorp/SampleModuleThemeDepend --backup-code

命令行将有以下输出信息：

	Code backup is starting...
	Code backup filename: 1435261098_filesystem_code.tgz (The archive can be uncompressed with 7-Zip on Windows systems)
	Code backup path: /var/www/html/magento2/var/backups/1435261098_filesystem_code.tgz
	[SUCCESS]: Code backup completed successfully.Removing frontend/ExampleCorp/SampleModuleTheme, frontend/ExampleCorp/SampleModuleThemeDepend from database
	Loading composer repositories with package information
	Updating dependencies (including require-dev)
	Removing frontend/ExampleCorp/SampleModuleTheme, frontend/ExampleCorp/SampleModuleThemeDepend from Magento codebase
	  - Removing ExampleCorp/sample-module-theme-depend (dev-master)
	Removing ExampleCorp/SampleThemeDepend
	  - Removing ExampleCorp/sample-module-theme (dev-master)
	Removing ExampleCorp/SampleTheme
	Writing lock file
	Generating autoload files
	Cache cleared successfully.
	Alert: Generated static view files were not cleared. You can clear them using the --clear-static-content option.
	Failure to clear static view files might cause display issues in the Admin and storefront.
	Disabling maintenance mode

<div class="bs-callout bs-callout-info" id="info">
  <p>To uninstall a Magento {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}Admin{% endglossarytooltip %} theme, you must also remove it from your component's {% glossarytooltip 2be50595-c5c7-4b9d-911c-3bf2cd3f7beb %}dependency injection{% endglossarytooltip %} configuration, <code>&lt;component root directory>/etc/di.xml</code>.</p>
</div>

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
*	[卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>