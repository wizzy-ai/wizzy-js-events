[<<  Back To List](/)


# BEFORE_AUTOCOMPLETE_PRODUCTS_RENDER

**When Executed ? :**  This event is triggered before the autocomplete products are rendered.

 **Purpose**: It allows for the modification of the autocomplete response products data before rendering.
 
Below are examples illustrating how to utilize this event.

### Round-off Selling Price
On the frontend, you are seeing selling prices like 775.53 RS or 523.36 RS, but you want to show prices like 776.00 RS or 523.00 RS. You can use the following logic:

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_PRODUCTS_RENDER, function(data) {
    data.products.forEach((product) => {
        product.sellingPrice = Math.round(parseFloat(product.sellingPrice)).toFixed(2);
    });
    return data;
});
```

### Change Top-Products-Title
By default, you will see 'Top Products' as the title of the autocomplete products section. If you want to give a custom title, you can add the following logic to your code:


```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_PRODUCTS_RENDER, function (data) {
    data.topProductsTitle = "Top Pics";
    return data;
});
```

### Add new field in products data
Suppose you want to show a 'New Arrival' banner on autocomplete products which have the 'new_arrival' tag. You can add the following logic to your code:

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_PRODUCTS_RENDER, function(data) {
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

###  Sample `data` of BEFORE_AUTOCOMPLETE_PRODUCTS_RENDER

```javascript
{
    "products": [
        {
            "images": [
                "https://cdn.shopify.com/s/files/1/0648/3066/9017/products/9780008470807.jpg.e7f012c0b6.999xx_360x.jpg?v=1680668197"
            ],
            "groupId": "",
            "isVisibleInAllVariants": true,
            "finalPrice": null,
            "discount": "0.00",
            "colors": [],
            "url": "https://www.testing.in/products/book-of-numbers-from-the-creator-of-the-1-bestselling-here-we-are",
            "discountPercentage": 0,
            "sellingPrice": "650.00",
            "totalReviews": null,
            "mainImage": "https://cdn.shopify.com/s/files/1/0648/3066/9017/products/9780008470807.jpg.e7f012c0b6.999xx_360x.jpg?v=1680668197",
            "sizes": [],
            "avgRatings": 0,
            "price": "650",
            "name": "Book of Numbers: From the creator of the# 1 bestselling Here We Are",
            "inStock": true,
            "attributes": [
               {
                    "values": [
                        {
                            "variationId": 8148381696217,
                            "inStock": true,
                            "value": [
                                "3-5 Years , 4-5 years , Book of Numbers: From the creator of the# 1 bestselling Here We Are , Books , BOOKS5 , Early Learning , Kids Books , kids books 4-5 years"
                            ]
                        }
                    ],
                    "name": "Tags",
                    "id": "product_tags"
                },
                {
                    "values": [
                        {
                            "variationId": 8148381696217,
                            "inStock": true,
                            "value": [
                                "Kids Books"
                            ]
                        }
                    ],
                    "name": "sub_category",
                    "id": "product_value_tags_sub_category"
                },
                
            
            ],
            "id": "43857803477209",
            "categories": [
                {
                    "image": "",
                    "name": "3-5 Years",
                    "id": "3-5-years",
                    "parentId": "",
                    "url": "https://www.testing.in/collections/3-5-years"
                },
                {
                    "image": "",
                    "name": "Early Learning",
                    "id": "early-learning",
                    "parentId": "",
                    "url": "https://www.testing.in/collections/early-learning"
                },        
            ],
            "sku": [
                "bk0461119",
                "0461119"
            ],
            "brand": "",
            "subTitle": "3-5 Years",
            "displayAddtoCart": true,
            "displayQuickView": false,
            "cart": {
                "action": "undefinedproduct/8148381696217/",
                "uenc": "dW5kZWZpbmVkcHJvZHVjdC84MTQ4MzgxNjk2MjE3Lw==",
                "searchResponseId": "efc318b0-379c-11ef-8352-0a6a11aebf00"
            },
            "author": "",
            "newSellingPrice": "650",
            "singleVarientGroupId": "43857803477209"
        },
    ],
    "total": 10000,
    "topProductsTitle": "Top Products",
    "isForDefault": false,
    "tSettings": {}
}
```