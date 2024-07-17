[<<  Back To List](/)


# PRODUCTS_RESULTS_RENDERED

**When Executed ? :** This event is triggered after products are rendered on search, autocomplete and collection page.

 **Purpose**: It allows for adding custom event listeners on elements.

Below are examples illustrating how to utilize this event.

## Open a Modal When Clicking on the Add to Cart Button

Suppose you want to open a pop-up modal when clicking on the add-to-cart button. You can write logic like this:


```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.PRODUCTS_RESULTS_RENDERED, function (data) {
    document.querySelectorAll('.add-to-cart').forEach(button => {
        button.addEventListener('click', function() {
            document.querySelector('.cart-popup').classList.remove('d-none');
        });
    });
    return data;
});
```

##  Sample `data` of PRODUCTS_RESULTS_RENDERED

```javascript
{}
```