[<<  Back To List](/)


# AFTER_PRODUCTS_TRANSFORMED

**When Executed ? :** This event is triggered after the product data is modified by Wizzy's frontend library as per the app configuration.

**Purpose**: It allows for modifying or adding new fields in the product data.

Below are examples illustrating how to utilize this event.


###  Round-off Price
On the frontend, you are seeing prices like 235.53 RS or 595.36 RS, but you want to show prices like 736.00 RS or 595.00 RS. You can use the following logic:

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.AFTER_PRODUCTS_TRANSFORMED, function(data) {
    data.forEach((product) => {
        product.price = Math.round(parseFloat(product.price)).toFixed(2);
    });
    return data;
});
```

### How to add new field in products data ?
**EX.1**
Suppose you want to show a 'Best Seller' banner on products that have the 'best_seller' tag. You can add the following logic to your code:

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.AFTER_PRODUCTS_TRANSFORMED, function(data) {
    data.forEach((product) => {
        let attributes = product.attributes;
        attributes.forEach((attribute) => {
            if (attribute.id === "product_tags") {
                product.isBestSeller = attribute.values[0].value[0].includes('beast_seller');
            }
        });
    });
    return data;
});
```

**EX.2**
Suppose you want to show the vendor of the products. You can add the following logic to your code:

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.AFTER_PRODUCTS_TRANSFORMED, function(data) {
    data.forEach((product) => {
        let attributes = product.attributes;
        product.vendor="";
        attributes.forEach((attribute) => {
            if (attribute.id === "product_vendor") {
                product.vendor = attribute.values[0].value[0];
            }
        });
    });
    return data;
});
```
Now, you can use the vendor variable to the wizzy's product template.

### Hide 'price' in products
```javascript
window.wizzyConfig.events.registerEvent(
    window.wizzyConfig.events.allowedEvents.AFTER_PRODUCTS_TRANSFORMED,
    function (data) {
        data.forEach((product) => {
                product.price = NULL;
            });
        return data;
    }
);
```

###  Sample `data` of AFTER_PRODUCTS_TRANSFORMED

```javascript
[{product1_data}, {product2_data}, {product3_data}, ...]
```