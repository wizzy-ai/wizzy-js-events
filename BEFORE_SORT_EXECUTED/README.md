[<<  Back To List](/)


# BEFORE_SORT_EXECUTED

**When Executed ? :** This event is triggered when the sort order is changed from the search page or collection page.

 **Purpose**: It allows for the modification of the sort payload. 
 
Below are examples illustrating how to utilize this event.

### Modify Sort Order

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_SORT_EXECUTED, function (data) {
     data.order = "desc"
    return data;
});
```


##  Sample `data` of BEFORE_SORT_EXECUTED

```javascript
{
    "value": "createdAt",
    "order": "asc"
}
```