---
group: install_cli
subgroup: 99_contrib
title: 添加或更新组件
menu_title: 添加或更新组件
menu_order: 5
menu_node:
version: 2.0
github_link: install-gde/install/cli/dev_add-update.md
functional_areas:
  - Install
  - System
  - Setup
---

A contributing developer updates 组件 by specifying 组件 and their versions in Magento's `composer.json`. 

To update components if you're *not* a contributing developer, see <a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">Updating the Magento application and 组件</a>.

You can either add a `require` section to `composer.json` or you can use the `composer require` command as follows:

1.	Log in to the Magento server, or switch to, the {% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento文件系统所有者{% endglossarytooltip %}.
2.	Change to the directory to which you cloned the Magento application. 例如，

		cd /var/www/magento2

You have the following options:

### Use the `composer require` command
命令用法：

	composer require <vendor>/<name>:<version>

例如，

	composer require example/module:1.0.0

Wait while {% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %} updates dependencies and installs the component.

### Add a `require` section to `composer.json`
Open `composer.json` in a text editor.

Add a `require` section like the following:

```JSON
	"require": {
		"<vendor>/<name>": "<version>",
		"<vendor>/<name>": "<version>"
	}
```

Save your changes to `composer.json`, exit the text editor, and enter `composer update`

### For more information
If you have issues, see <a href="https://getcomposer.org/doc/articles/troubleshooting.md" target="_blank">Composer troubleshooting</a>.

<!-- ABBREVIATIONS -->

*[contributing developer]: A developer who contributes code to the Magento 2 CE codebase
