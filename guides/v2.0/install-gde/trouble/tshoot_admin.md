---
group: install_trouble
title: 登录到Magento管理面板时出错
version: 2.0
github_link: install-gde/trouble/tshoot_admin.md
functional_areas:
  - Install
  - System
  - Setup
---

### Details

  The requested URL /magento2index.php/admin/admin/dashboard/index/key/0c81957145a968b697c32a846598dc2e/ was not found on this server.

Note the lack of a slash character between `magento2` and `index.php` in the {% glossarytooltip a05c59d3-77b9-47d0-92a1-2cbffe3f8622 %}URL{% endglossarytooltip %}.

### Solution

The base URL is not correct. The base URL must:

* Start with `http://`或`https://`
* End with a slash (`/`)
* Match the case of the `web/unsecure/base_url` record in the `core_config_data` database table

Re-run the installation using a valid value.