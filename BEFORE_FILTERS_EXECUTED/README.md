[<<  Back To List](/)


# BEFORE_FILTERS_EXECUTED

**When Executed ? :** This event is triggered before the Filter API call.

 **Purpose**: It allows for the modification of the filter API request payload data. 
 
Below are examples illustrating how to utilize this event.

## Add/Change Sort Order?
For the search and collection pages, 'Relevance' will be the default sort order. If you want to change 'Relevance' to 'createdAt', you can write code like this:


```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_FILTERS_EXECUTED, function (data) {
    if(data.filters.sort.length && data.filters.sort[0].field == 'relevance'){
        data.filters.sort[0] = {"field": "createdAt", "order": "asc"};
    }
    return data;
});
```

If you want to add 'createdAt' as a second-level sort, you can write logic like this:


```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_FILTERS_EXECUTED, function (data) {
    if(data.filters.sort.length && data.filters.sort[0].field == 'relevance'){
        data.filters.sort.push({"field": "createdAt", "order": "asc"});
    }
    return data;
});
```
Now your first-level sort will be 'Relevance' and the second-level sort will be 'createdAt'. Instead of createdAt, you can use other available fields like `sellinPrice`.

**NOTE:** If you have multiple sorts, the algorithm first sorts the products according to the first-level sort. If there are ties among some products, it will apply the second-level sort to resolve those ties.


## Show Out-of-stock products in order
By default, our app shows out-of-stock (OOS) products at the end of the list. If you want to see them in their actual order, you can write the following logic:

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_FILTERS_EXECUTED, function(data) {
    data.filters.showOOSProductsInOrder = "true";
    return data;
});
```

##  Sample `data` of BEFORE_FILTERS_EXECUTED

```javascript
{
    "filters": "{\"attributes\":{},\"categories\":[\"books\"],\"page\":1,\"sort\":[{\"field\":\"sellingPrice\",\"order\":\"asc\"},{\"field\":\"product_books_sortOrder:float\",\"order\":\"asc\"}],\"type\":\"CATEGORY_PAGE\",\"facets\":[{\"label\":\"Category\",\"key\":\"product_value_tags_category\",\"position\":\"left\",\"order\":0},{\"label\":\"Sub Category\",\"key\":\"product_value_tags_sub_category\",\"position\":\"left\",\"order\":1},{\"label\":\"Genre\",\"key\":\"product_value_tags_genre\",\"position\":\"left\",\"order\":2},{\"label\":\"Format\",\"key\":\"product_book_binding_custom\",\"position\":\"left\",\"order\":3},{\"label\":\"Product Type\",\"key\":\"product_value_tags_product_type\",\"position\":\"left\",\"order\":4},{\"label\":\"Author\",\"key\":\"product_books_author_1_custom\",\"position\":\"left\",\"order\":5},{\"label\":\"Language\",\"key\":\"product_books_language_custom\",\"position\":\"left\",\"order\":6},{\"label\":\"Price\",\"key\":\"sellingPrice\",\"position\":\"left\",\"order\":7}],\"getAllVariants\":\"false\",\"swatch\":[],\"currency\":\"INR\",\"productsCount\":24,\"attributeFacetValuesLimit\":50,\"showOOSProductsInOrder\":\"true\"}",
    "group": "categoryPage"
}
```