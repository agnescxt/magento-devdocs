---
group: config-guide
subgroup: 04_CLI
title: 部署静态视图文件
menu_title: 部署静态视图文件
menu_node:
menu_order: 300
version: 2.0
github_link: config-guide/cli/config-cli-subcommands-static-view.md
redirect_from: /guides/v1.0/config-guide/cli/config-cli-subcommands-static-view.html
functional_areas:
  - Configuration
  - System
  - Setup
---

{% include config/cli-intro.md %}

## 概述 of static view files deployment {#config-cli-static-overview}
The static view files deployment command enables you to write {% glossarytooltip 363662cb-73f1-4347-a15e-2d2adabeb0c2 %}static files{% endglossarytooltip %} to the Magento file system when the Magento software is set for <a href="{{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#production-mode">production mode</a>.

The term *static view file* refers to the following:

-   "Static" means it can be cached for a site (that is, the file is not dynamically generated). Examples include images and {% glossarytooltip 6c5cb4e9-9197-46f2-ba79-6147d9bfe66d %}CSS{% endglossarytooltip %} generated from LESS.
-   "View" refers to the presentation layer (from MVC).

Static view files are located in the `<your Magento install dir>/pub/static` directory, and some are cached in the `<your Magento install dir>/var/view_preprocessed` directory as well.

Static view file deployment is affected by Magento modes as follows:

-   **[Default]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#default-mode)** and **[developer]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#developer-mode)** modes: Magento generates them on demand, but the rest are cached in a file for speed of access.
-   **[Production]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#production-mode)** mode: Static files are *not* generated or cached.

You must write static view files to the Magento file system manually using the command discussed in this topic; after that, you can restrict permissions to limit your vulnerabilities and to prevent accidental or malicious overwriting of files.

<div class="bs-callout bs-callout-warning" markdown="1">
_Developer mode only_: When you install or enable a new module, it might load new JavaScript, CSS, layouts, and so on. To avoid issues with static files, you must clean the old files to make sure you get all the changes for the new {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}.

You can clean generated static view files in several ways. Refer to [清除静态文件缓存 topic for details]({{ page.baseurl }}/howdoi/clean_static_cache.html) for more information.
</div>

## 部署静态视图文件 {#config-cli-subcommands-xlate-dict}
To deploy static view files:

1.  Log in to the Magento server as, or <a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">switch to</a>, the {% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento文件系统所有者{% endglossarytooltip %}.
2.  Delete the contents of `<your Magento install dir>/pub/static`.
3.  Run the static view files deployment tool `<your Magento install dir>/bin/magento setup:static-content:deploy`.
<!-- 4.	Set read-only file permissions for the `pub/static` directory, its subdirectories, and files. -->

	<div class="bs-callout bs-callout-info" id="info" markdown="1">
  If you enable static view file merging in the Magento Admin, the `pub/static` directory system must be writable.
	</div>

命令参数：

	magento setup:static-content:deploy <lang> ... <lang> [--dry-run]

The following table explains this command's parameters and values.

<table>
	<tbody>
		<tr>
			<th>Option</th>
			<th>描述</th>
			<th>是否必需?</th>
		</tr>
	<tr>
		<td>&lt;languages&gt;</td>
		<td><p>Space-separated list of <a href="http://www.loc.gov/standards/iso639-2/php/code_list.php" target="_blank">ISO-639</a> language codes for which to output static view files. (Default is <code>en_US</code>.)</p>
		<p>You can find the list by running <code>magento info:language:list</code>.</p></td>
	<td><p>否</p></td>
	</tr>
		<tr>
		<td>--dry-run</td>
		<td><p>Include to view the files output by the tool without outputting anything.</p></td>
		<td><p>否</p></td>
	</tr>
	</tbody>
</table>

例如， to deploy static view files for the `pt_BR` language:

	magento --ansi setup:static-content:deploy pt_BR

The following are some sample messages that display to indicate successful deployment:

	Requested languages: pt_BR
	=== frontend -> Magento/luma -> pt_BR ===
	... progress indicator ...
	Successful: 1613 files; errors: 0

	=== frontend -> Magento/blank -> pt_BR ===
	... progress indicator ...
	Successful: 1620 files; errors: 0

	=== adminhtml -> Magento/backend -> pt_BR ===
	... progress indicator ...
	Successful: 1626 files; errors: 0

	=== Minify templates ===
	... progress indicator ...
	Successful: 858 files modified
	---
	New version of deployed files: 1430773903

## 故障排除 the static view files deployment tool {#view-file-trouble}
[Install the Magento software first]({{ page.baseurl }}/install-gde/bk-install-guide.html); otherwise, you cannot run the static view files deployment tool.

**Symptom**: The following error is displayed when you run the static view files deployment tool:

	ERROR: You need to install the Magento application before running this utility.

**Solution**:

Use the following steps:

1.  Install the Magento software in any of the following ways:

    -   [命令行]({{ page.baseurl }}/install-gde/install/cli/install-cli.html)
    -   [Setup wizard]({{ page.baseurl }}/install-gde/install/web/install-web.html)

2.  Log in to the Magento server as, or switch to, the [Magento文件系统所有者]({{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html).
3.  Delete the contents of `<your Magento install dir>/pub/static` directory.
4.  <a href="#config-cli-subcommands-xlate-dict">Run the static view files deployment tool</a>.
<!-- 4.	Set read-only file permissions for the `pub/static` directory, its subdirectories, and files. -->

	<!-- <div class="bs-callout bs-callout-info" id="info">
		<span class="glyphicon-class">
  		<p>If you enable static view file merging in the Magento Admin, the <code>pub/static</code> directory system must be writable.</p></span>
	</div> -->

## Tips for developers customizing the static content deployment tool
When creating a custom implementation of the {% glossarytooltip a3e37235-4e8b-464f-a19d-4a120560206a %}static content{% endglossarytooltip %} deployment tool, do not use non atomic writing to files that should be available on the client side. Otherwise, those files might be loaded on the client side with partial content.

One of the options for making it atomic, is writing to files stored in a temporary directory and copying or moving them to the destination directory (from where they are actually loaded to client side) once writing is over. For details about writing to files see [http://php.net/manual/en/function.fwrite.php](http://php.net/manual/en/function.fwrite.php){:target="\_blank"}.

Please note, that the default Magento implementation of `\Magento\Framework\Filesystem\Directory\WriteInterface::writeFile` uses non-atomic write to file.

## 相关主题

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">配置和执行定时任务</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">代码编译器</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">设置Magento的模式</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-urn.html">统一资源名称(URN)高亮</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">创建软链接到LESS文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">转换布局的XML文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
