# Wizzy Events Docs

## Developers Guide
This document provides details on how to customize data, UI/UX before/after rendering, tailoring it to your needs. Below is a list of events triggered in various scenarios. You can register these events in your JavaScript file and modify it as per your need.

## Why Events?
Through events, you can change or modify actual API response data used for frontend rendering through mustache.

Specific events will be triggered based on interactions with Wizzy elements. If you want to customize these interactions, you can use our event structure.




## Allowed Events
Click on the event name to see detailed explanations and examples.


|                 Scope                 |               Event Name                  |                  When Executed ?                     |    Purpose             |
|----------------------------------------|-------------------------------------------|--------------------------------------------------|---------------------------
| Init                                   | [BEFORE_INIT](/BEFORE_INIT/README.md)     | Before Wizzy gets initialized.                  | To change the Wizzy app settings variable.|
| Search                                 | [BEFORE_SEARCH_EXECUTED](/BEFORE_SEARCH_EXECUTED/README.md) | Before the search API call.    |Modify the request payload of the search API .  |
| Filter                                 | [BEFORE_FILTERS_EXECUTED](/BEFORE_FILTERS_EXECUTED/README.md) | Before the filter API call. |Modify the request payload of the filter API.|
| Sort                                   | [BEFORE_SORT_EXECUTED](/BEFORE_SORT_EXECUTED/README.md) | Before the filter API call. | Modify the sort payload.|
| Autocomplete                           | [BEFORE_AUTOCOMPLETE_EXECUTED](/BEFORE_AUTOCOMPLETE_EXECUTED/README.md) | Before the autocomplete API call. | Modify the request payload of the autocomplete API.|
| Autocomplete                           | [BEFORE_AUTOCOMPLETE_PRODUCTS_RENDER](/BEFORE_AUTOCOMPLETE_PRODUCTS_RENDER/README.md) | Before the autocomplete products render | Modify the products data.|
| Autocomplete                           | [BEFORE_AUTOCOMPLETE_WRAPPER_RENDER](/BEFORE_AUTOCOMPLETE_WRAPPER_RENDER/README.md) | Just before autocomplete HTML render | To modify the direct HTML. |
| Autocomplete                           | [BEFORE_AUTOCOMPLETE_RENDER](/BEFORE_AUTOCOMPLETE_RENDER/README.md) |  Before the autocomplete wrapper render  | Modify JSON object of autocomplete data. |
| Autocomplete                           | [BEFORE_AUTOCOMPLETE_SUGGESTIONS_RENDER](/BEFORE_AUTOCOMPLETE_SUGGESTIONS_RENDER/README.md) |Before autocomplete suggestion render | Modify the JSON object of autocomplete suggestions.|
| All APIs                               | [AFTER_WIZZY_API_RESPONDED](/AFTER_WIZZY_API_RESPONDED/README.md) | After all API calls | Modify the server response. |
| Swatches                               | [PRODUCT_SWATCH_CLICKED](/PRODUCT_SWATCH_CLICKED/README.md) | Products's swacth clicked | Modify the Swatch payload.|
| NoResultsPage                          | [EMPTY_RESULTS_RENDERED](/EMPTY_RESULTS_RENDERED/README.md) | Triggered after an empty page is rendered| Add custom pop-ups |
| Search Results Page & Products Listing Page| [AFTER_PRODUCTS_TRANSFORMED](/AFTER_PRODUCTS_TRANSFORMED/README.md) |After product data is modified by Wizzy's frontend library | Modify Products JSON object. |
| Search Results Page & Products Listing Page| [VIEW_RENDERED](/VIEW_RENDERED/README.md) | Triggered after view is rendered. | Attach custom events. |
| Search Results Page & Products Listing Page| [PRODUCTS_CACHED_RESULTS_RENDERED](/PRODUCTS_CACHED_RESULTS_RENDERED/README.md) | Navigates from the product page to the search page. | Attach custom events. |
| Search Results Page & Products Listing Page   | [PRODUCTS_RESULTS_RENDERED](/PRODUCTS_RESULTS_RENDERED/README.md) | Triggered after products are rendered. | To attach custom events to product elements. |
| Filter                                     | [AFTER_FILTER_ITEM_CLICKED](/AFTER_FILTER_ITEM_CLICKED/README.md) | Will get HTML content of autocomplete wrapper |
|                            | [BEFORE_LAZY_INIT](/BEFORE_LAZY_INIT/readme.md) | Will get HTML content of autocomplete wrapper |
|                            | [BEFORE_PRODUCTS_RESULTS_RENDERED](/BEFORE_PRODUCTS_RESULTS_RENDERED/readme.md) | Will get HTML content  |
|                            | [BEFORE_RENDER_RESULTS](/BEFORE_RENDER_RESULTS/README.md) | WHOLE OBJECT SEARCH AND FILTER| |



## Register the event 
To use an event you must register it first and push it into the `window.onWizzyLoaded` array. You can take a reference from the example below.


```javascript
let wizzyEvents = function () {
   window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_INIT, function (data) {
       // Handle event 1 here
       return data;
    });
   window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.VIEW_RENDERED, function (data) {
        // Handle event 2 here
        return data;
    });
}

window.onWizzyLoaded.push(wizzyEvents);
```

## Usage of Events:
Suppose you want add class to search modal  when user enters the search query and hit the enter button. 

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_SEARCH_EXECUTED, function (data) {
      let searchModel = document.querySelector('.search-model');
      searchModel.classList.add('d-none');
    return data;
});
```
To see more examples, please use the event table above. By clicking on an event name, you will get a detailed explanation with examples.

## Notes:
* Each event handler must return modified data.
* Please avoid duplicating events for optimization purposes. Reuse the same events when possible.
* Ensure there are no JavaScript syntax errors.
* If you’re not using Wizzy Frontend Library to render the frontend, these events will not function as expected. 