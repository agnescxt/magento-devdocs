---
group: compman
subgroup: 02_prereq
title: 在管理面板输入你的认证密钥
menu_title: 在管理面板输入你的认证密钥
menu_order: 2
menu_node:
version: 2.0
github_link: comp-mgr/prereq/prereq_auth-token.md
functional_areas:
  - Upgrade
---

<div class="bs-callout bs-callout-info" id="info">
	<p>To upgrade your {{site.data.var.ee}} version or to upgrade from {{site.data.var.ce}} to {{site.data.var.ee}}, you must be authorized to access the  {{site.data.var.ee}} repository. Contact <a href="http://support.magentocommerce.com" target="&#95;blank">Magento Support</a> if you have questions.</p>
</div>

To enter your [authentication keys]({{ page.baseurl }}/install-gde/prereq/connect-auth.html):

1.	Log in to the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %} as an administrator.
2.	Click **System** > Tools > **网页安装向导**.
3.	Click **System Configuration**.

	<img src="{{ site.baseurl }}/common/images/cman_system-config.png" width="550px">

4.	Enter your public and private authentication keys in the provided fields.
5.	Click **Save Config**.

	<img src="{{ site.baseurl }}/common/images/cman_keys.png" width="550px">
