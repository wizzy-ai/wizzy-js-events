[<<  Back To List](/)


# BEFORE_INIT

**When Executed ? :** This event is triggered before Wizzy's search and filter functionalities are initialized.

 **Purpose**: It allows for the modification of app configurations. 

Below are examples illustrating how to utilize this event.

### Change minQueryLength for search
  By default the value of minQueryLength is 3. It means after entering minimum 3 character search will show some result. You can set it betwwen 1 to 6.

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_INIT, function (data) {
    data.search.configs.general.minQueryLength = 1;
    return data;
});
```


### Change the number of products per page for a particular collection
 
Suppose your collection handle is 'xyz' and for that collection, you want to set the number of products per page to 15.
```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_INIT, function (data) {
   if(data.common.collectionHandle=='xyz')
      {
        data.search.configs.general.noOfProducts=15;
      }   
       return data;
});
```

### Keep a filter open after applying it on mobile

```javascript
window.wizzyConfig.events.registerEvent(window.wizzyConfig.events.allowedEvents.BEFORE_INIT, function (data) {
      data.filters.configs.keepOpenedInMobileAfterApply = true;
    return data;
});
```

###  Sample `data` of wizzyConfig
Preview/open the theme in which Wizzy is enabled. Open the inspect mode and enter `wizzyConfig` in the console. You will see data like below. You can access this data in the `BEFORE_INIT` event.
```javascript
{
    "filters": {
        "configs": {
            "keepOpenedInMobileAfterApply": true,
            "displayAsDrawer": false,
            "drawerPosition": "left"
        }
    },
    "credentials": {
        "apiKey": "testingapikey",
        "storeId": "testingstoreid"
    },
    "search": {
        "addToCart": {
            "data": [],
            "display": true,
            "method": "ajax"
        },
        "quickView": {
            "data": [],
            "display": false
        },
        "tileView": {
            "display": false
        },
        "addToWishlist": {
            "data": [],
            "display": true
        },
        "enabled": true,
        "input": {
            "dom": ".wizzy-search-input",
            "placeholder": "Search entire store here..."
        },
        "configs": {
            "general": {
                "dom": ".wizzy-main-content",
                "searchEndpoint": "/pages/search",
                "noOfProducts": 24,
                "includeOutOfStock": false,
                "displayAllVariants": false,
                "behaviour": "on_form_submmission",
                "formSubmissionBehaviour": "replace_columns_on_same_page",
                "minQueryLength": 1
            },
            "facets": {
                "configs": [
                    {
                        "label": "Category",
                        "key": "product_value_tags_category",
                        "position": "left",
                        "order": 1
                    },
                    {
                        "label": "Sub Category",
                        "key": "product_value_tags_sub_category",
                        "position": "left",
                        "order": 2
                    },
                ],
                "categoryDisplay": "list",
                "leftFacets": {
                    "collapsible": true,
                    "defaultCollapsed": true,
                    "firstLeftDefaultOpened": true
                },
                "filtersButtonMobile": {
                    "position": "bottom",
                    "offset": 0
                }
            },
            "sorts": {
                "configs": [
                    {
                        "label": "Relevance",
                        "field": "relevance",
                        "order": "asc"
                    },
                    {
                        "label": "Price: Low to High",
                        "field": "sellingPrice",
                        "order": "asc"
                    },
                ],
                "addBestSellingAsSecondSort": false,
                "bestSellingCategoryHandle": "wizzy-best-selling"
            },
            "swatches": {
                "configs": []
            },
            "pagination": {
                "type": "infinite_scroll",
                "moveToTopWidget": {
                    "add": false
                }
            },
            "noProductsFound": {
                "showProducts": true,
                "defaultPool": {
                    "method": "filters",
                    "expiry": "session",
                    "data": {
                        "productsCount": 50,
                        "categories": [
                            "harry-potter"
                        ]
                    }
                }
            }
        },
        "view": {
            "domSelector": ".wizzy-main-content",
            "noProductsFoundDOM": ".wizzy-main-content",
            "templates": {
                "literals": {
                    "emptyCategoryPageTitle": "We couldn`t find any Products for this Collection!",
                    "emptySearchResultPageTitle": "We couldn`t find any matches!"
                },
                "summary": "#wizzy-search-summary",
                "wrapper": "#wizzy-search-wrapper",
                "results": "#wizzy-search-results",
                "product": "#wizzy-search-results-product",
                "emptyResults": "#wizzy-search-empty-results",
                "emptyCollectionResults": "#wizzy-collection-empty-results",
                "facets": {
                    "common": "#wizzy-facet-block",
                    "item": "#wizzy-facet-item-common",
                    "rangeItem": "#wizzy-facet-range-item",
                    "commonRangeAboveItem": "#wizzy-facet-range-above-item",
                    "categoryItem": "#wizzy-facet-category-item",
                    "selectedItem": "#wizzy-selected-facet-item-common",
                    "selectedCommon": "#wizzy-selected-facets-block"
                },
                "pagination": "#wizzy-search-pagination",
                "sort": "#wizzy-search-sort"
            }
        }
    },
    "common": {
        "isLazyInit": false,
        "isOnLoadDOMInit": true,
        "lazyDOMConfig": {
            "searchInputIdentifiers": [
                {
                    "dom": ".section-header [name=\"q\"]",
                    "type": "text"
                }
            ],
            "contentDOMIdentifiers": [
                "#MainContent",
                ".main-content",
                "main"
            ],
            "identifiersToClickOnSearch": [
                ".search-modal__content .modal__close-button"
            ],
            "identifiersToHideOnSearch": []
        },
        "isOnCategoryPage": false,
        "isOnCategoryListing": false,
        "isOnProductViewPage": false,
        "hasToReplaceCollectionPages": true,
        "useCollectionHandleAsId": true,
        "categoryUrlKey": "",
        "currentProductId": "",
        "view": {
            "templating": {
                "mustache": {
                    "delimiters": [
                        "[[",
                        "]]"
                    ]
                }
            },
            "templates": {
                "progress": "#wizzy-progress",
                "select": "#wizzy-common-select",
                "literals": {
                    "sortBy": "Sort By"
                }
            }
        },
        "templateAttributes": []
    },
    "autocomplete": {
        "enabled": true,
        "searchBar": {
            "hasAnimatedPlaceholders": false,
            "animatedPlaceholders": []
        },
        "configs": {
            "general": {
                "openCategoryPage": true
            },
            "defaultBehaviour": {
                "suggestions": {
                    "enabled": false,
                    "displayRecent": true,
                    "displayTrending": true,
                    "defaultPool": [
                        {
                            "value": "Non Fiction",
                            "valueHighlighted": "Non Fiction",
                            "filters": [],
                            "payload": [],
                            "section": "categories"
                        },
                        {
                            "value": "Kids Books",
                            "valueHighlighted": "Kids Books",
                            "filters": [],
                            "payload": [],
                            "section": "categories"
                        },
                        {
                            "value": "Business & Management",
                            "valueHighlighted": "Business & Management",
                            "filters": [],
                            "payload": [],
                            "section": "categories"
                        }
                    ]
                },
                "topProducts": {
                    "enabled": true,
                    "displayRecent": "false",
                    "displayTrending": "false",
                    "defaultPool": {
                        "method": "filters",
                        "expiry": "session",
                        "data": {
                            "categories": [
                                "top-6"
                            ],
                            "productsCount": 10
                        }
                    }
                }
            }
        },
        "menu": {
            "suggestionsCount": 5,
            "alignment": "left",
            "noResultsBehaviour": "hide_menu",
            "noResultsText": "No results found.",
            "sections": [
                "categories"
            ],
            "firstSection": "categories",
            "categories": {
                "title": "Top Categories"
            },
            "others": {
                "title": "Trending Searches"
            },
            "brands": {
                "title": "Brands"
            },
            "view": {
                "menu": ".wizzy-autocomplete-wrapper",
                "selectable": "selectable",
                "searchterm": "searchterm",
                "position": "left",
                "text-wrapper": ".autocomplete-text-wrapper",
                "wrapper": ".wizzy-body-end-wrapper",
                "topProductsBlock": ".wizzy-autocomplete-top-products",
                "suggestionLink": ".autocomplete-link",
                "suggestionLabel": ".wizzy-autocomplete-label",
                "templates": {
                    "wrapper": "#wizzy-autocomplete-wrapper",
                    "suggestions": "#wizzy-autocomplete-suggestions",
                    "products": "#wizzy-autocomplete-topproducts"
                },
                "formSubmissionBehaviour": "replace_columns_on_same_page"
            }
        },
        "topProducts": {
            "suggestTopProduts": true,
            "count": 9,
            "title": "Top Products"
        },
        "pages": {
            "title": "Pages"
        },
        "recentSearches": {
            "title": "Recent Searches"
        }
    },
    "pageStore": {
        "suggestionFilters": [],
        "searchInputValue": "",
        "filteringFor": "",
        "selectedSortMethod": {
            "label": "Relevance",
            "field": "relevance",
            "order": "asc"
        }
    },
    "store": {
        "currency": {
            "code": "INR",
            "symbol": "₹"
        }
    },
    "analytics": {
        "enabled": true,
        "generateEvents": true,
        "configs": {
            "general": []
        },
        "endpoints": {
            "clicks": "",
            "sessions": "",
            "views": "",
            "conversions": ""
        }
    },
    "gridFilters": {
        "enabled": false,
        "filters": []
    },
    "events": {
        "allowedEvents": {
            "AFTER_PRODUCTS_TRANSFORMED": "afterProductsTransformed",
            "BEFORE_AUTOCOMPLETE_EXECUTED": "beforeAutocompleteExecuted",
            "BEFORE_SEARCH_EXECUTED": "beforeSearchExecuted",
            "AFTER_FILTER_ITEM_CLICKED": "afterFilterItemClicked",
            "BEFORE_FILTERS_EXECUTED": "beforeFiltersExecuted",
            "BEFORE_SORT_EXECUTED": "beforeSortExecuted",
            "PRODUCT_SWATCH_CLICKED": "productSwatchClicked",
            "VIEW_RENDERED": "viewRendered",
            "PRODUCTS_RESULTS_RENDERED": "productsResultsRendered",
            "PRODUCTS_CACHED_RESULTS_RENDERED": "productsCachedResultsRendered",
            "BEFORE_PRODUCTS_RESULTS_RENDERED": "beforeProductsResultsRendered",
            "EMPTY_RESULTS_RENDERED": "emptyResultsRendered",
            "BEFORE_INIT": "beforeInit",
            "BEFORE_LAZY_INIT": "beforeLazyInit",
            "BEFORE_RENDER_RESULTS": "beforeRenderResults",
            "BEFORE_AUTOCOMPLETE_PRODUCTS_RENDER": "beforeAutocompleteProductsRender",
            "BEFORE_AUTOCOMPLETE_WRAPPER_RENDER": "beforeAutocompleteWrapperRender",
            "BEFORE_AUTOCOMPLETE_RENDER": "beforeAutocompleteRender",
            "BEFORE_AUTOCOMPLETE_SUGGESTIONS_RENDER": "beforeAutocompleteSuggestionsRender",
            "AFTER_WIZZY_API_RESPONDED": "afterWizzyApiResponded",
            "BEFORE_PRODUCTS_BY_IDS_RESULTS_RENDERED": "beforeProductsByIdsResultsRendered",
            "BEFORE_PRODUCTS_BY_IDS_HTML_RENDERED": "beforeProductsByIdsHtmlRendered"
        },
        "registeredEvents": []
    }
}
```