[<<  Back To List](/)


# BEFORE_AUTOCOMPLETE_SUGGESTIONS_RENDER

**When Executed ? :** This event is triggered before the autocomplete suggestions render.

 **Purpose**: It allows for changing the autocomplete suggestion's JSON object data.

Below are examples illustrating how to utilize this event.


### Change the Suggestion Label for the Default Autocomplete View

Suppose on the frontend you are seeing 'xyz-abc' in the default suggestions, but you want to show it as 'xyz abc'. You can write code like this:
```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_AUTOCOMPLETE_SUGGESTIONS_RENDER, function (data) {
   if (data.isForDefault) {
        data.suggestions.forEach((suggestion) => {
          if (suggestion.label === 'xyz-abc') {
            suggestion.label = "xyz abc";
          }
        });
   }
   return data;
});
```
**Note:** You will get the `isForDefault` value as true when you just click on the search bar without entering any word, which is considered the default autocomplete behavior. In all other cases, you will get the value as false.

###  Sample `data` of BEFORE_AUTOCOMPLETE_SUGGESTIONS_RENDER

```javascript
   {
    "suggestions": [
        {
            "label": "Top Categories",
            "group": "categories",
            "isHead": true,
            "hasLabelPath": false,
            "searchTerm": "",
            "index": 0,
            "isRecentSearch": false,
            "isRecentSearchHead": false
        },
        {
            "label": "Business & Management",
            "labelPath": [],
            "hasLabelPath": false,
            "group": "categories",
            "isHead": false,
            "index": 2,
            "searchTerm": "business & management",
            "isRecentSearch": false,
            "isTrendingSearch": false
        }
    ],
    "hasSuggestions": true,
    "tSettings": {},
    "isDisplayingRecentSearches": true,
    "isForDefault": true
}
```