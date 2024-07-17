[<<  Back To List](/)


# EMPTY_RESULTS_RENDERED

**When Executed ? :** This event is triggered after an empty page is rendered.

**Purpose**: It allows for adding custom pop-up or model.

Below are examples illustrating how to utilize this event.


### Open pop-up on empty result page.

To open a pop-up on an empty results page, you can use the following JavaScript code:
```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.EMPTY_RESULTS_RENDERED, function (data) {
   document.querySelector('.empty-result-popup').classList.remove('d-none');
   return data;
});
```

###  Sample `data` of EMPTY_RESULTS_RENDERED

```javascript
{}
```