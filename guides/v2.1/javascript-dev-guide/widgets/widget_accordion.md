---
group: jsdg
subgroup: 3_Widgets
title: 手风琴菜单小工具
menu_order: 1
menu_title: 手风琴菜单小工具
version: 2.1
github_link: javascript-dev-guide/widgets/widget_accordion.md
redirect_from:
  - guides/v2.0/frontend-dev-guide/javascript/widget_accordion.html
  - guides/v1.0/frontend-dev-guide/javascript/widget_accordion.html
---

<h2>概述</h2>

Magento 手风琴菜单小工具 is an {% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %} of the <a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_tabs.html" target="_blank">Magento 标签页小工具</a>.

Accordions are generally used to break content into multiple sections that can be swapped to save space.

The accordion {% glossarytooltip f0dcf847-ce21-4b88-8b45-83e1cbf08100 %}小工具{% endglossarytooltip %} source is <a href="{{ site.mage2000url }}lib/web/mage/accordion.js" target="_blank">lib/web/mage/accordion.js</a>.

<h2 id="accordion_init">Initialize the 手风琴菜单小工具</h2>

<h3>Initialize accordion in JS 组件</h3>

<h4>Initialize accordion with <code>data-*</code> attributes specified</h4>
Generally the 手风琴菜单小工具 is instantiated like following:
<pre>
$("#element").accordion();
</pre>

Where:
<ul>
<li><code>#element</code> is the selector of the element for accordion is initialized.</li>
<li><code>#element</code> has children with the following attributes specified: 

<ul>
<li><code>data-role="title"</code>
</li>
<li><code>data-role="content"</code></li>
</ul>
</li>
</ul>

Optionally, you can specify the following:
<ul>
<li>If you want the trigger to be different from the title, add the <code>data-role="content"</code> attribute for the element</li>

<li>To have the content updated using Ajax, add the <code>data-ajax="true"</code> attribute for the element containing the {% glossarytooltip a05c59d3-77b9-47d0-92a1-2cbffe3f8622 %}URL{% endglossarytooltip %} for request.
</li>
</ul>

Accordions support arbitrary markup, but the following requirements should be kept:

<ol>
<li>Titles and contents are specified in the same order in DOM: first title, then contents.</li>

<li>The header, trigger and content are specified, either by adding the <code>data-*</code> attributes for the corresponding children elements or by specifying these elements with selectors as options.</li>
</ol>

Mark-up 例如:

{%highlight html%}
<div id="element">
    <div data-role="collapsible">
        <div data-role="trigger">
            <span>Title 1</span>
        </div>
    </div>
    <div data-role="content">Content 1</div>

    <div data-role="collapsible">
        <div data-role="trigger">
            <span>Title 2</span>
        </div>
    </div>
    <div data-role="content">Content 2</div>

    <div data-role="collapsible">
        <div data-role="trigger">
            <span>Title 3</span>
        </div>
    </div>
    <div data-role="content">Content 3</div>
</div>

<script>
    require([
        'jquery',
        'accordion'], function ($) {
        $("#element").accordion();
    });
</script>

{%endhighlight%}


<h4>Initialize accordion with option</h4>
You can specify the header, content, trigger as options when you initialize the widget.
例如:
<pre>
$("#element").accordion({
    header : "#title-1",
    content : "#content-1",
    trigger : "#trigger-1",
    ajaxUrlElement: "a"
 });
</pre>

<h3>Initialize accordion in a template</h3>

The 手风琴菜单小工具 can be initialized using the <code>data-mage-init</code> attribute or `<script>` element, as described in <a href="{{ page.baseurl }}/javascript-dev-guide/javascript/js_init.html#data_mage_init" target="_blank">JavaScript initialization</a>.


<h2 id="accordion_options">Options</h2>
Accordion options coincide with <a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_tabs.html#fedg_tabs_options" target="_blank">Magento Tabs options</a>, plus the following custom ones:
<ul>
<li><a href="#collaps_active">active</a></li>
<li><a href="#collaps_multi">multipleCollapsible</a></li>
<li><a href="#collaps_open">openOnFocus</a></li>
</ul>

<h3 id="collaps_active"><code>active</code></h3>

Defines which tab is active when the widget gets instantiated.

**Type**: Array, String

**Default value**: `0`

Example of the accordion initialization with the <code>active</code> option specified:
<pre>
$("#element").accordion({ active: "0 1"});
$("#element").accordion({ active: [0,1]});
</pre>


<h3 id="collaps_multi"><code>multipleCollapsible</code></h3>
Defines if multiple panels can be expanded at the same time.

**Type**: Boolean

**Default value**: `false`

Example of the accordion initialization with the <code>multipleCollapsible</code> option specified:
<pre>
$("#element").accordion({ multipleCollapsible: false});
</pre>
Get or set the <code>multipleCollapsible</code> option, after initialization:
<pre>
//getter
var multipleCollapsible = $("#element").accordion("option","multipleCollapsible");

//setter
$("#element").tabs("option","multipleCollapsible",false);
</pre>

<h3 id="collaps_open"><code>openOnFocus</code></h3>

For keyboard navigation defines if the accordion expands when the title gets in focus.

**Type**: Boolean

**Default value**: `false`


<h2 id="accordion_methods">Methods</h2>
手风琴菜单小工具 options and keyboard interaction mostly coincide with the Magento 标签页小工具 methods.

The custom accordion methods are the following:

<ul>
<li><a href="#meth_act">activate()</a></li>
<li><a href="#meth_deact">deactivate()</a></li>
</ul>

<h3 id="meth_act"><code>activate(index)</code></h3>
Activate a tab with the specified `index`.

**Type**: Number, Array.

If no `index` is passed, all panels are activated.

Code 例如:
<pre>
$( "#element" ).accordion( "activate" );
$( "#element" ).accordion( "activate", 1 );
$( "#element" ).accordion( "activate", [0,1]);
</pre>

<h3 id="meth_deact"><code>deactivate(index)</code></h3>
Deactivate a tab with the specified `index`.


**Type**: Number, Array.

If no index is passed, all panels are deactivated.

Code 例如:

<pre>
$( "#element" ).accordion( "deactivate" );
$( "#element" ).accordion( "deactivate", 1 );
$( "#element" ).accordion( "deactivate", [0,1]);
</pre>
