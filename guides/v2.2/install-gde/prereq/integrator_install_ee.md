---
group: install_pre
subgroup: S_Integrator
title: 获取Magento EE工程包
menu_title: 获取Magento EE工程包
menu_order: 4
menu_node:
version: 2.2
github_link: install-gde/prereq/integrator_install_ee.md
functional_areas:
  - Install
  - System
  - Setup
---

To get the {{site.data.var.ee}} metapackage:

1.	See [(集成工程师)集成安装]({{ page.baseurl }}/install-gde/prereq/integrator_install.html) first.
2.	Make sure you know your support portal user name and password.

	If you don't remember it, contact Magento Support before you continue.
3.	Log in to your Magento server as, or switch to, the <a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">Magento文件系统所有者</a>.
4.	Change to the web server docroot directory, or to a directory you've configured as a virtual host docroot.
5.	输入下面的命令：

		composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition <installation directory name>

	When prompted, enter your <a href="{{ page.baseurl }}/install-gde/prereq/connect-auth.html">authentication keys</a>. Your *public key* is your username; your *private key* is your password.

	The following error indicates your tokens are incorrect:

		  Could not find package magento/project-enterprise-edition with version 2.0.0

	This command creates the project and downloads dependencies for it. The project is in a directory named `<installation directory name>` if you provided the parameter or `project-enterprise-edition` if you did not.

	<div class="bs-callout bs-callout-info" id="info">
  		<p>If the following error displays, see <a href="{{ page.baseurl }}/install-gde/trouble/tshoot_composer-fail.html">troubleshooting</a>:</p>
  		<pre>file_get_contents(app/etc/NonComposerComponentRegistration.php): failed to open stream: No such file or directory</pre>
	</div>

## 安装B2B扩展 (optional)
Change to your installation directory and enter the following command to update your `composer.json` file and install the {{site.data.var.b2b}} extension:

    composer require magento/extension-b2b

When prompted, enter your <a href="{{ page.baseurl }}/install-gde/prereq/connect-auth.html">authentication keys</a>. Your *public key* is your username; your *private key* is your password.

<div class="bs-callout bs-callout-info" markdown="1">
If you installed EE prior to installing B2B, run the following commands after Composer finishes updating modules:

    bin/magento setup:upgrade

    bin/magento setup:di:compile

    bin/magento setup:static-content:deploy
</div>

After installing Magento, you'll need to [configure the B2B module]({{ page.baseurl }}/comp-mgr/install-extensions/b2b-installation.html#configure-b2b).

{% include install/file-system-perms-before_22.md %}

#### 下一步
Install the Magento software:

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">Command line</a>
*	<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">Setup Wizard</a>
