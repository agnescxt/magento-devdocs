---
group: config-guide
subgroup: 09_Varnish
title: 安装Varnish
menu_title: 安装Varnish
menu_order: 5
menu_node:
version: 2.2
github_link: config-guide/varnish/config-varnish-install.md
functional_areas:
  - Configuration
  - System
  - Setup
---

<h2 id="config-varnish-install">安装Varnish</h2>
Installing the Varnish software is beyond the scope of this guide. For more information about installing Varnish, see:

*	<a href="http://wiki.mikejung.biz/Varnish" target="_blank">installation wiki</a>
*	<a href="https://www.varnish-cache.org/docs" target="_blank">Varnish 安装向导s</a>
*	<a href="http://www.tecmint.com/install-varnish-cache-web-accelerator" target="_blank">How to install Varnish (Tecmint)</a>

<div class="bs-callout bs-callout-info" id="info" markdown="1">
This topic is written for Varnish on CentOS and Apache 2.2. If you're setting up Varnish in a different environment, some commands are likely different. Consult the preceding documentation for more information.

If you intend to install Varnish modules (vmods), such as saint mode, you should install Varnish by compiling the code, rather than installing from a package. See [Saint mode]({{ page.baseurl }}/config-guide/varnish/config-varnish-advanced.html#saint) for more details.
</div>

<h2 id="config-varnish-version">Confirm your Varnish version</h2>
Enter the following command to display the version of Varnish you're running:

	varnishd -V

A sample follows:

	varnishd (varnish-4.0.3 revision b8c4a34)
	Copyright (c) 2006 Verdens Gang AS
	Copyright (c) 2006-2014 Varnish Software AS

Make sure the version is 4.x or 5.x before continuing. If you are running version 3.x, you must upgrade to a supported version. Consult the Varnish installation documentation for more information.

### 下一步
<a href="{{ page.baseurl }}/config-guide/varnish/config-varnish-configure.html">配置Varnish和你的web服务器</a>
