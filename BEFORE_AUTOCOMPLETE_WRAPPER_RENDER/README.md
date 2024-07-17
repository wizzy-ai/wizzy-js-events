[<<  Back To List](/)


# BEFORE_AUTOCOMPLETE_WRAPPER_RENDER

**When Executed ? :**  This event is triggered just before the HTML rendering of the autocomplete wrapper.

 **Purpose**: It allows for the direct modification of the HTML of the autocomplete wrapper.
 
Below are examples illustrating how to utilize this event.

### Swap the 'Others' and 'Categories' order 
By default, we are showing 'categories' first, and then 'other'. You can reverse this by adding this logic.
```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_WRAPPER_RENDER, function(data) {
    // Convert the string to HTML elements
    const parser = new DOMParser();
    const suggestionHtml = parser.parseFromString(data.suggestions, 'text/html');

    // Get the suggestions list
    const suggestionsList = suggestionHtml.querySelector('.autocomplete-suggestions-list');

    // Separate items under Others and Categories
    const othersItems = [];
    const categoriesItems = [];

    suggestionsList.querySelectorAll('.autocomplete-item').forEach((item) => {
        const head = item.previousElementSibling;
        if (head && head.classList.contains('autocomplete-item-head')) {
            if (head.getAttribute('data-index') === '1') {
                othersItems.push(item);
            } else if (head.getAttribute('data-index') === '0') {
                categoriesItems.push(item);
            }
        }
    });

    // Clear the existing list
    suggestionsList.innerHTML = '';

    // Append Others items first
    othersItems.forEach((item) => {
        suggestionsList.appendChild(item);
    });

    // Append Categories items
    categoriesItems.forEach((item) => {
        suggestionsList.appendChild(item);
    });

    // Convert back to string
    const modifiedSuggestion = suggestionHtml.body.innerHTML;

    data.suggestions = modifiedSuggestion;

    return data;
});
```

### Change Top-Products-Title
By default, you will see 'Top Products' as the title of the autocomplete products section. If you want to give a custom title, you can add the following logic to your code:


```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_WRAPPER_RENDER, function (data) {
    data.topProductsTitle = "Top Pics";
    return data;
});
```

### Add new field in products data
Suppose you want to show a 'New Arrival' banner on autocomplete products which have the 'new_arrival' tag. You can add the following logic to your code:

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_WRAPPER_RENDER, function(data) {
    data.products.forEach((product) => {
        let attributes = product.attributes;
        attributes.forEach((attribute) => {
            if (attribute.id === "product_tags") {
                product.isNewArrival = attribute.values[0].value[0].includes('new_arrival');
            }
        });
    });
    return data;
});
```
You can use `isNewArrival` in Mustache templates to conditionally show a 'New Arrival' banner.

###  Sample `data` of BEFORE_AUTOCOMPLETE_WRAPPER_RENDER

```javascript
{
    "suggestions": "\n    <div class=\"wizzy-autocomplete-suggestions\">\n        <ul class=\"autocomplete-suggestions-list\">\n            <li class=\"autocomplete-item-head\" data-index=\"0\">\n                Top Categories\n            </li><!-- ending of autocomplete-item-head -->\n            <li class=\"autocomplete-item\">\n                <a data-selectable=\"true\" data-searchterm=\"book of the month\" href=\"#\"\n                   class=\"autocomplete-link\"\n                   data-index=\"0\">\n\n\n                    <span class='wizzy-autocomplete-label'> <em>Boo</em>k of the Month </span>\n                        <span class=\"autocomplete-text-wrapper\"></span>\n                </a><!-- ending of autocomplete-link -->\n            </li><!-- ending of autocomplete-item -->\n          s<!-- ending of autocomplete-item -->\n        </ul>\n    </div><!-- ending of autocomplete-suggestions -->\n",
    "isMenuHidden": true,
    "topProducts": "\n  <div class=\"wizzy-autocomplete-top-products\">\n        <p class=\"top-products-title\">Top Products</p>\n        <ul class=\"autocomplete-top-products\">\n\n           <li\n  class=\"\n    wizzy-result-product wizzy-product-43823240020185\n    \"\n  title=\"Boo! A Collection of Thirteen Stories That Will Send a Chill Down Your Spine\"\n  data-id=\"43823240020185\"\n  >\n  <span class=\"wizzy-product-variation-loader-bg\"></span>\n  <span class=\"wizzy-product-variation-loader\"></span>\n\n  <a href=\"https://www.crossword.in/products/boo-a-collection-of-thirteen-stories-that-will-send-a-chill-down-your-spine-1\" class=\"wizzy-result-product-item\">\n          \n    <div class=\"result-product-item-image\">\n      <img src=\"https:&#x2F;&#x2F;cdn.shopify.com&#x2F;s&#x2F;files&#x2F;1&#x2F;0648&#x2F;3066&#x2F;9017&#x2F;products&#x2F;getimage_26b4ee98-dc68-494e-a1d8-aa19850f41c3_360x.jpg?v&#x3D;1678858916\" class=\"product-item-image\" loading=\"lazy\">\n    </div>\n    <!-- ending of result-product-item-image -->\n    <div class=\"result-product-item-image hover-image\">\n      <img src=\"https:&#x2F;&#x2F;cdn.shopify.com&#x2F;s&#x2F;files&#x2F;1&#x2F;0648&#x2F;3066&#x2F;9017&#x2F;products&#x2F;getimage_26b4ee98-dc68-494e-a1d8-aa19850f41c3_360x.jpg?v&#x3D;1678858916\" class=\"product-item-image\" loading=\"lazy\">\n    </div>\n    <!-- ending of result-product-item-image -->\n    <div class=\"result-product-item-info\">\n      <p class=\"product-item-title\">Boo! A Collection of Thirteen Stories That Will Send a Chill Down Your Spine</p>\n      <p class=\"product-item-author\">Shinie Antony</p>\n      \n      <div class=\"wizzy-product-item-price-reviews-wrapper\">\n        <div class=\"wizzy-product-item-reviews\">\n\n        </div>\n\n        <div class=\"wizzy-product-item-price \">\n           ₹299\n           \n           \n        </div>\n\n\n        <!-- <div class=\"wizzy-add-to-cart-container\">\n          <form method=\"post\" action=\"/cart/add\" class='wizzy-add-to-cart-box\n'>\n            <input type=\"hidden\" name=\"id\" value=\"43823240020185\">\n            <input min=\"1\" type=\"hidden\" id=\"quantity\" name=\"quantity\" value=\"1\">\n            <input type=\"submit\" value=\"ADD TO BAG\" class=\"wizzy-tocart-button btn button\">\n          </form>\n        </div> -->\n        \n        \n        \n        <!-- ending of wizzy-product-actions -->\n      </div>\n      <!-- ending of wizzy-product-item-price-reviews-wrapper -->\n    </div>\n    <!-- ending of result-product-item-info -->\n  </a>\n  <!-- ending of wizzy-result-product-item -->\n  <!-- <span class=\"wizzy iWishAddColl iwishCol\" data-variant=\"43919012659417\" data-product=\"8173503906009\" data-ptitle=\"Robodog\"><svg version=\"1.1\" xmlns=\"http://www.w3.org/2000/svg\" xmlns:xlink=\"http://www.w3.org/1999/xlink\" width=\"16\" height=\"16\" viewBox=\"0 0 16 16\"><path fill=\"#000000\" d=\"M11.8 1c-1.682 0-3.129 1.368-3.799 2.797-0.671-1.429-2.118-2.797-3.8-2.797-2.318 0-4.2 1.882-4.2 4.2 0 4.716 4.758 5.953 8 10.616 3.065-4.634 8-6.050 8-10.616 0-2.319-1.882-4.2-4.2-4.2z\"></path></svg></span> -->\n</li>\n<!-- ending of wizzy-result-product -->\n\n\n\n \n<!-- ending of wizzy-result-product -->\n\n\n        </ul><!-- ending of autocomplete-top-products -->\n        <div class=\"autocomplete-top-products-view-more\">\n            <button type=\"button\" class=\"btn btn--small wizzy-autocomplete-top-products-view-more\">\n                View More\n            </button>\n        </div>\n   <div style=\"\n    color: white;\n\"> .</div>\n    </div><!-- ending of top-products -->\n",
    "hasSuggestions": true,
    "tSettings": {}
}
```