---
group: fedg
subgroup: B_Layouts
title: 覆盖一个布局
menu_title: 覆盖一个布局
menu_order: 5
version: 2.0
github_link: frontend-dev-guide/layouts/layout-override.md
redirect_from: /guides/v1.0/frontend-dev-guide/layouts/layout-override.html
functional_areas:
  - Frontend
---

<h2 id="fedg_layout_override_overview">这里有什么</h2>

Not all layout customizations can be performed by <a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-extend.html" target="_blank">extending</a> existing layouts. If the amount of customizations is large, you can use the overriding function for the needed layout file. This means that the new file that you place in the theme will be used instead of the parent <a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-overview.html#layout-loc" target="_blank">theme</a> layout file of <a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-overview.html#layout-loc" target="_blank">base</a> {% glossarytooltip 73ab5daa-5857-4039-97df-11269b626134 %}布局{% endglossarytooltip %} file.

In this article, <a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-types.html#layout-types-page" target="_blank">page layouts</a>, <a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-types.html#layout-types-conf" target="_blank">page configurations</a>,以及<a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-types.html#layout-types-gen" target="_blank">generic layouts</a> are referred to as *layout files*, as the mechanism of overriding is similar for all of them.


Layout files with instructions that override the default or parent {% glossarytooltip d2093e4a-2b71-48a3-99b7-b32af7158019 %}主题{% endglossarytooltip %} files are referred to as *overriding layout files*.


<h2>Examples of customizations that involve overriding layouts</h2>
Examples of customizations that involve overriding layouts:

*	Suppressing method invocation.

	<div class="bs-callout bs-callout-info" id="info">
		<p>Overriding is not necessary if a block has a method that cancels the effect of the originally invoked method. In this case, you can customize the layout by adding a layout file where the canceling method is invoked.</p>
	</div>

*	Modifying method arguments.
*	Canceling block/container removal using the `remove` attribute.
*	Setting {% glossarytooltip 8c0645c5-aa6b-4a52-8266-5659a8b9d079 %}XML{% endglossarytooltip %} attributes of blocks and containers.

	<div class="bs-callout bs-callout-info" id="info">
		<p>Certain attributes, like <code>htmlClass</code>, <code>htmlId</code>, <code>label</code> attributes can be changed in <a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-extend.html" target="_blank">extending layouts</a>.</p>
	</div>
*	Removing block arguments.
*	Modifying and suppressing <a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-overview.html#handle" target="_blank">handles</a> inclusion.
*	Removing all handle instructions by declaring an overriding layout file with an empty handle.


<h2 id="fedg_layout_override_howto">How to override a layout</h2>

This section discusses how to override:

*	<a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-overview.html#layout-loc" target="_blank">Base layout</a>
*	<a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-overview.html#layout-loc" target="_blank">Theme layout</a>

<h3 id="fedg_layout_override_default">Override base layouts</h3>

To add an overriding base layout file (to override a base layout provided by the module):


2.	Put a layout file with the same name in the following location:

<pre>
&lt;theme_dir&gt;
&nbsp;&nbsp;|__/&lt;Namespace_Module&gt;
&nbsp;&nbsp;&nbsp;&nbsp;|__/layout
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__/override
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__/base
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--&lt;layout1&gt;.xml
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--&lt;layout2&gt;.xml

</pre>

These files override the following layouts:

<ul>
<li><code>&lt;module_dir&gt;/view/frontend/layout/&lt;layout1&gt;.xml</code></li>
<li><code>&lt;module_dir&gt;/view/frontend/layout/&lt;layout2&gt;.xml</code></li>
</ul>

<h3 id="fedg_layout_override_theme">Override theme layouts</h3>

To add an overriding theme file (to override a parent theme layout):

2.	Put a layout file with the same name in the following location:

<pre>
&lt;theme_dir&gt;
&nbsp;&nbsp;|__/&lt;Namespace_Module&gt;
&nbsp;&nbsp;&nbsp;&nbsp;|__/layout
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__/override
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__/theme
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__/&lt;Parent_Vendor&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__/&lt;parent_theme&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--&lt;layout1&gt;.xml
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--&lt;layout2&gt;.xml
</pre>

These files override the following layouts:

<ul>
<li><code>&lt;parent_theme_dir&gt;/&lt;Namespace&gt;_&lt;Module&gt;/layout/&lt;layout1&gt;.xml</code></li>
<li><code>&lt;parent_theme_dir&gt;/&lt;Namespace&gt;_&lt;Module&gt;/layout/&lt;layout2&gt;.xml</code></li>
</ul>

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p>To override page layout files, use 'page_layout' directory name instead of 'layout'</p></span>
</div>


<h2 id="override-mistake">Customization mistakes</h2>

Although the layout overriding mechanism provides great customization flexibility, it's possible to use it to add logically irrelevant changes. We strongly recommend you not make the following changes:

*	Changing block name or alias. The name of a block should not be changed, and neither should the alias of a block remaining in the same parent element.
*	Changing handle inheritance. 例如， you should not change the page type parent handle.

#### 相关主题:

*	<a href="{{ page.baseurl }}/frontend-dev-guide/layouts/layout-extend.html" target="_blank">扩展一个布局</a>
*	<a href="{{ page.baseurl }}/frontend-dev-guide/themes/theme-create.html" target="_blank">Create a theme</a>
*	<a href="{{ page.baseurl }}/frontend-dev-guide/layouts/xml-instructions.html" target="_blank">布局指令</a>
