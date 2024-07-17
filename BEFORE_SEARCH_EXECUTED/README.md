[<<  Back To List](/)


# BEFORE_SEARCH_EXECUTED

**When Executed ? :** This event is triggered before the Search API call.

 **Purpose**: It allows for the modification of the search API request payload data. 
 
Below are examples illustrating how to utilize this event.

### Add/Change Sort Order?
For the search results, 'Relevance' will be the default sort order. If you want to change 'Relevance' to 'sellingPrice', you can write code like this:


```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_SEARCH_EXECUTED, function (data) {
    if(data.sort.length && data.sort[0].field == 'relevance'){
        data.sort[0] = {"field": "sellingPrice", "order": "asc"};
    }
    return data;
});
```

If you want to add 'sellingPrice' as a second-level sort, you can write logic like this:


```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_SEARCH_EXECUTED, function (data) {
    if(data.sort.length && data.sort[0].field == 'relevance'){
        data.sort.push({"field": "sellingPrice", "order": "asc"});
    }
    return data;
});
```
Now your first-level sort will be 'Relevance' and the second-level sort will be 'sellingPrice'. Instead of sellingPrice, you can use other available fields like `createdAt`, `bestSeller`.

**NOTE:** If you have multiple sorts, the algorithm first sorts the products according to the first-level sort. If there are ties among some products, it will apply the second-level sort to resolve those ties.

### Change attributeFacetValuesLimit
By default, the application shows a maximum of 20 filters for the facet. If you want to increase this limit to 50 (max limit is 50), you can modify the attributeFacetValuesLimit value.

Add the following code snippet to your configuration to update the limit:
```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_SEARCH_EXECUTED, function (data) {
    data.attributeFacetValuesLimit = 50;
       return data;
});
```


###  Sample `data` of BEFORE_SEARCH_EXECUTED

```javascript
{
    "q": "book",
    "currency": "INR",
    "includeOutOfStock": "false",
    "getAllVariants": "false",
    "productsCount": 24,
    "facets": "[{\"label\":\"Category\",\"key\":\"product_value_tags_category\",\"position\":\"left\",\"order\":0},{\"label\":\"Sub Category\",\"key\":\"product_value_tags_sub_category\",\"position\":\"left\",\"order\":1},{\"label\":\"Genre\",\"key\":\"product_value_tags_genre\",\"position\":\"left\",\"order\":2},{\"label\":\"Format\",\"key\":\"product_book_binding_custom\",\"position\":\"left\",\"order\":3},{\"label\":\"Product Type\",\"key\":\"product_value_tags_product_type\",\"position\":\"left\",\"order\":4},{\"label\":\"Author\",\"key\":\"product_books_author_1_custom\",\"position\":\"left\",\"order\":5},{\"label\":\"Language\",\"key\":\"product_books_language_custom\",\"position\":\"left\",\"order\":6},{\"label\":\"Price\",\"key\":\"sellingPrice\",\"position\":\"left\",\"order\":7}]",
    "swatch": "[]",
    "minQueryLength": 1,
    "sort": "[{\"field\":\"sellingPrice\",\"order\":\"asc\"}]",
    "attributeFacetValuesLimit": 50
}
```