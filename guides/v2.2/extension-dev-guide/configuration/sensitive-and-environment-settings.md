---
group: extension-dev-guide
subgroup: Configuration
title: 敏感数据和环境变量
menu_title: 敏感数据和环境变量
menu_order: 1000
version: 2.2
github_link: extension-dev-guide/configuration/sensitive-and-environment-settings.md
functional_areas:
  - Configuration
---

This topic discusses how third-party developers can create Magento组件 that designate configuration settings as being sensitive, system-specific, or both.

## Guidelines

Use the following guidelines to determine which settings to designate as sensitive, system-specific, or both.

Magento stores these settings in `<Magento root dir>/app/etc/env.php`.
Do not include this file in source control.

### Sensitive values

_Sensitive_ configuration values hold restricted or confidential information.

Examples of sensitive information include:

*	Keys (such as API keys)
*	User names and passwords
*	E-mail addresses
*	Any personally identifiable information (e.g., address, phone number, date of birth, government identification number, 等.)

### Environment or system-specific values

_Environment_ or _system-specific_ values are unique to the system where Magento is deployed.

Examples of environment or system-specific values include:

*	URLs
*	IP addresses
*	Ports
*	Host names
*	Domain names
*	Paths (e.g., custom paths, proxy host, proxy port)
*	"modes" (e.g, sandbox mode, debug mode, test mode)
*	SSL (only for non-payment)
*	E-mail recipients
*	Administrative settings between systems (e.g., password expiration limits)

## How to specify values as sensitive or system-specific

Add a reference to [`Magento\Config\Model\Config\TypePool`][typepool]{:target="_blank"} to the [`di.xml`][di-xml] file to specify either a system-specific or sensitive configuration value.


### 示例: Sensitive settings

{% highlight php startinline=true %}
<type name="Magento\Config\Model\Config\TypePool">
   <arguments>
      <argument name="sensitive" xsi:type="array">
         <item name="payment/test/password" xsi:type="string">1</item>
      </argument>
   </arguments>
</type>
{% endhighlight %}

After specifying the sensitive setting, use the following commands to verify it:

    php bin/magento cache:clean
    php bin/magento app:config:dump

A message similar to the following is displayed:

    The configuration file doesn't contain sensitive data for security reasons. Sensitive data can be stored in the following environment variables:
    CONFIG__DEFAULT__PAYMENT__TEST__PASWORD for payment/test/password
    Done.

### 示例: System-specific settings

{% highlight php startinline=true %}
<type name="Magento\Config\Model\Config\TypePool">
   <arguments>
      <argument name="environment" xsi:type="array">
         <item name="catalog/search/searchengine/port" xsi:type="string">1</item>
      </argument>
   </arguments>
</type>
{% endhighlight %}

### Sensitive, system-specific setting

To set a configuration setting as both sensitive and system-specific, create two entries with the `name` property for `argument` set to `sensitive` for one entry and `environment` for the other.

#### 相关主题

* [配置导入器][config-importers]
*	[di.xml文件][di-xml]
*	[开发者指引]({{ page.baseurl }}/extension-dev-guide/intro/developers_roadmap.html)
*	[依赖注入]({{ page.baseurl }}/extension-dev-guide/depend-inj.html)

[typepool]: {{ site.mage2200url }}app/code/Magento/Config/Model/Config/TypePool.php
[di-xml]: {{ page.baseurl }}/extension-dev-guide/build/di-xml-file.html
[config-importers]: {{ page.baseurl }}/extension-dev-guide/configuration/importers.html
