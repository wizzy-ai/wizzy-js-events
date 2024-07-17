[<<  Back To List](/)


# PRODUCTS_CACHED_RESULTS_RENDERED

**When Executed ? :** This event is triggered when one navigates from the product page to the search/collection page.

 **Purpose**: It allows for adding custom event listeners on elements.

Below are examples illustrating how to utilize this event.

### Example

Suppose you have added custom logic to handle the wishlist in the VIEW_RENDERED event like this:

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.VIEW_RENDERED, function (data) {
    document.querySelectorAll('.my-wishlist').forEach(button => {
        button.addEventListener('click', function() {
            // Wishlist logic
        });
    });
    return data;
});
```
Now, if you go to the PDP page through the search page and then return to the result page, your wishlist functionality will not work. You need to attach the same logic inside the `PRODUCTS_CACHED_RESULTS_RENDERED` event.

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.VIEW_RENDERED, function (data) {
    document.querySelectorAll('.my-wishlist').forEach(button => {
        button.addEventListener('click', function() {
            //whishlist logic
        });
    });
    return data;
});
```

###  Sample `data` of VIEW_RENDERED

```javascript
{}
```