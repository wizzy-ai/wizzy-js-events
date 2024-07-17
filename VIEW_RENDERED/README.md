[<<  Back To List](/)


# VIEW_RENDERED

**When Executed ? :** This event is triggered when you interact with the result page (applying sort and filter, pagination, swatch click), and a new view is rendered.

**Purpose**: It allows for adding custom event listeners on elements.

Below are examples illustrating how to utilize this event.

### Customize CSS for a specific case

Suppose you want to apply specific CSS when there is only one product in the response. You can write the logic like this:

```javascript
if (payload.data.api === 'filter' || payload.data.api === 'search') {
    let productList = payload.data.response.payload.result;
    if (productList.length === 1) {
        document.body.classList.add('wizzy-single-product-result');
    } else {
        document.body.classList.remove('wizzy-single-product-result');
    }
}
```

###  Sample `data` of VIEW_RENDERED
```javascript

//For Autocomplete API
{
    "response": {
       ....data....
      
    },
    "api": "autocomplete",
    "requestId": "f5b56d19-796e-4f81-b2df-7fbfd9043367",
    "responseId": "575d0cc2-384e-11ef-a8d5-0a6a11aebf00"
}

-----------------------------------------------------------------------
//For search API
{
    "response": {
       ....data....
      
    },
    "api": "search",
    "requestId": "f5b56d19-796e-4f81-b2df-7fbfd9043367",
    "responseId": "575d0cc2-384e-11ef-a8d5-0a6a11aebf00"
}
------------------------------------------------------------------------
//For filter API
{
    "response": {
       ....data....
      
    },
    "api": "filter",
    "requestId": "f5b56d19-796e-4f81-b2df-7fbfd9043367",
    "responseId": "575d0cc2-384e-11ef-a8d5-0a6a11aebf00"
}
```