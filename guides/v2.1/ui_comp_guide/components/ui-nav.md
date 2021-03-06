---
group: UI_组件_guide
subgroup: 组件
title: 导航栏组件
menu_title: 导航栏组件
version: 2.1
github_link: ui_comp_guide/components/ui-nav.md
---

## 概述

The 导航栏组件 implements tabs navigation.

See the [管理面板用到的设计模式和库 (Tabs)]({{ page.baseurl }}/pattern-library/containers/tabs/tabs.html) topic for information about the UI design patterns that can be implemented using the 导航栏组件.

## Configuration options

Extends all `uiComponent` and `collapsible` configuration.

Nav-specific options:

<table>
  <tr>
    <th>Option </th>
    <th>描述</th>
    <th>Type</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><code>collapsible</code></td>
    <td>Enables/disables the collapsible functionality.</td>
    <td>Boolean</td>
    <td><code>false</code></td>
  </tr>
  <tr>
    <td><code>component</code></td>
    <td>The path to the component’s JS constructor, in terms of RequireJS.</td>
    <td>String</td>
    <td><code>Magento_Ui/js/form/组件/tab_group</code></td>
  </tr>
  <tr>
    <td><code>opened</code></td>
    <td>Initial collapsible state, if the collapsible functionality is enabled.</td>
    <td>Boolean</td>
    <td><code>true</code></td>
  </tr>
  <tr>
    <td><code>template</code></td>
    <td>The path to the component’s <code>.html</code> template.</td>
    <td>String</td>
    <td><code>ui/tab</code></td>
  </tr>
</table>
