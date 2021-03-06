---
group: mrg
subgroup: 20_Enterprise Edition
ee_only: true
title: Magento_CheckoutStaging模块
menu_title: CheckoutStaging
menu_order: 2
version: 2.2
ee_only: true
github_link: mrg/ee/CheckoutStaging.md
---

The Magento_CheckoutStaging {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %} is a part of the staging functionality in {{site.data.var.ee}}.
It extends the {% glossarytooltip 278c3ce0-cd4c-4ffc-a098-695d94d73bde %}checkout{% endglossarytooltip %} functionality and enables you to use it in the staging preview mode.

## Implementation details

The Magento_CheckoutStaging模块 extends the following Magento_Checkout模块 functionality to be used in the staging preview mode:

- Disables an order creation
- Creates a demo {% glossarytooltip 77e19d0d-e7b1-4d3d-9bad-e92fbb9fb59a %}quote{% endglossarytooltip %}
- Deletes the demo quote using cron

Configuration options:

- The `preview_quota_lifetime` parameter in the `Magento/CheckoutStaging/etc/config.xml` sets the lifetime of the demo quote.
- The `schedule` parameter in the `Magento/CheckoutStaging/etc/crontab.xml` sets a launch schedule of the cron.

### 安装 details

The Magento_CheckoutStaging模块 makes irreversible changes in a database during installation. You cannot uninstall this module.

## Dependencies

You can find the list of modules that have dependencies on the Magento_CheckoutStaging模块 in the `require` section of the `composer.json` file. The file is located in the root directory of the module.

## Extension points

{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}Extension{% endglossarytooltip %} points enable extension developers to interact with the Magento_CheckoutStaging模块. For more information about the Magento extension mechanism, see [Magento plug-ins](http://devdocs.magento.com/guides/v2.2/extension-dev-guide/plugins.html).

[The Magento dependency injection mechanism](http://devdocs.magento.com/guides/v2.2/extension-dev-guide/depend-inj.html) enables you to override the functionality of the Magento_CheckoutStaging模块.

## Additional information

You can track [backward incompatible changes made in a {{site.data.var.ee}} mainline after the Magento 2.0 release](http://devdocs.magento.com/guides/v2.0/release-notes/backward-incompatible-changes/commerce.html).
