[<<  Back To List](/)


# AFTER_WIZZY_API_RESPONDED

**When Executed ? :** This event is triggered before all types of API calls.

**Purpose**: It allows for changing the server-side response.

Below are examples illustrating how to utilize this event.


### How to check the type of the API
```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.AFTER_WIZZY_API_RESPONDED, function (data) {
   if (data.api == 'Saerch') {
    //Add your logic.
   }
   else if(data.api == "autocomplete")
   {
     //Add your logic.
   }
   return data;
});
```
### Hide 'price' for autocomplete
```javascript
window.wizzyConfig.events.registerEvent(
    window.wizzyConfig.events.allowedEvents.AFTER_WIZZY_API_RESPONDED,
    function (data) {
        if (data.api === 'autocomplete') {
            data.response?.payload?.products?.result?.forEach((product) => {
                product.price = 0;
            });
        }
        return data;
    }
);

```

###  Sample `data` of AFTER_WIZZY_API_RESPONDED

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
```