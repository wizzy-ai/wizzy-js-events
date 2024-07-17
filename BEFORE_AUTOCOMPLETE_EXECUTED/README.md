[<<  Back To List](/)


# BEFORE_AUTOCOMPLETE_EXECUTED

**When Executed ? :** This event is triggered before the autocomplete API call.

 **Purpose**: It allows for the modification of the autocomplete API request payload data. 
 
Below are examples illustrating how to utilize this event.

### Change Sort Order
For the autocomplete, 'Relevance' will be the default sort order. If you want to change 'Relevance' to 'sellingPrice', you can write code like this:


```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_EXECUTED, function (data) {
    if(data.sort.length && data.sort[0].field == 'relevance'){
        data.sort[0] = {"field": "sellingPrice", "order": "asc"};
    }
    return data;
});
```

### Change getAllVariants setting
By default Autocomplete API returns single variant per product, Set this to true if you want Autocomplete API to return all the variants of a product in single API response.

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_EXECUTED, function (data) {
    data.getAllVariants = "true";
    return data;
});
```

###  Sample `data` of BEFORE_AUTOCOMPLETE_EXECUTED

```javascript
{
    "q": "book",
    "currency": "INR",
    "suggestionsCount": 5,
    "includeOutOfStock": "false",
    "getAllVariants": "false",
    "minQueryLength": 1,
    "productsCount": 9,
    "sections": "[{\"key\":\"categories\"}]",
    "sort": "[{\"field\":\"relevance\",\"order\":\"asc\"}]",
    "swatch": "",
    "facets": ""
}
```