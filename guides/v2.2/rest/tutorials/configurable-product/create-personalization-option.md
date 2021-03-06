---
layout: tutorial
group: rest
title: 步骤5. Create the personalization option
menu_title: 步骤5. Create the personalization option
menu_order: 50
level3_subgroup: configurable-product-tutorial
version: 2.2
github_link: rest/tutorials/configurable-product/create-personalization-option.md
functional_areas:
  - Integration
---

Let's add a text box to the product page that allows the customer to add his name (up to 15 characters) to the back of shirt.

The `product_sku` is the `sku` of the configurable product. The `sku` specified in the payload is a string that is appended to the `product_sku` when a customer decides to purchase this option. Likewise, the `price` supplied in the payload is added to the configurable product price.

**接口**

`POST V1/products/options`

**载荷**
``` json
{
  "option": {
    "product_sku": "MS-Champ",
    "title": "Add Your Name (Max 15 Characters)",
    "type": "field",
    "sort_order": 1,
    "is_require": false,
    "price": 10,
    "price_type": "fixed",
    "sku": "Personalized",
    "max_characters": 15
  }
}

```

**响应**

``` json
{
    "product_sku": "MS-Champ",
    "option_id": 7,
    "title": "Add Your Name (Max 15 Characters)",
    "type": "field",
    "sort_order": 1,
    "is_require": false,
    "price": 10,
    "price_type": "fixed",
    "sku": "Personalized",
    "max_characters": 15
}
```

## Verify this step

* Log in to the Luma website and select **Catalog > Products**. Click on the **Champ Tee** configurable product and expand the **Customizable Options** section.

  ![Product page with configurable and simple products]({{ page.baseurl }}/rest/images/options-section.png)

* On the Luma store front page, search for `Champ`. Then click on the Champ Tee product.

  ![Search results]({{ page.baseurl }}/rest/images/add-your-name.png)

  <div class="bs-callout bs-callout-info" id="info" markdown="1">
  If the personalization option is not displayed, go to the **Champ Tee** configuration product page in Admin and set  **Stock Status** to **In Stock**.
  </div>

  ## Congratulations! You've finished.
  {:.no_toc}

  ## 相关主题

  * [使用REST API的订单处理教程]({{ page.baseurl }}/get-started/order-tutorial/order-intro.html)
