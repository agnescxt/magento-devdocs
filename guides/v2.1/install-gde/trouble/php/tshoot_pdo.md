---
group: install_trouble
subgroup: 03_install
title: 安装期间出现PDO致命错误
menu_title: 安装期间出现PDO致命错误
menu_node:
menu_order: 21
version: 2.1
github_link: install-gde/trouble/php/tshoot_pdo.md
redirect_from:
  - /guides/v1.0/install-gde/trouble/tshoot_pdo.html
  - /guides/v2.0/install-gde/trouble/tshoot_pdo.html
functional_areas:
  - Install
  - System
  - Setup
---

### Details

	PHP Fatal error:  Class 'PDO' not found in /var/www/html/magento2/setup/module/Magento/Setup/src/Module/Setup/ConnectionFactory.php on line 44

### Solution:

Make sure you installed all required PHP extensions (<a href="{{ page.baseurl }}/install-gde/prereq/php-centos.html">CentOS</a>, <a href="{{ page.baseurl }}/install-gde/prereq/php-ubuntu.html">Ubuntu</a>). 

