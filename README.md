# Assignment Summer School Polymer 2017 (ITAC0249)

## Template : 

Polymer Starter Kit

## Components 

* iron-ajax
* paper-search-panel
* iron-localstorage
* paper-button

## Functions

Application main function is search youtube videos with google api, and save selected items to local storage.

### Search youtube with google api

```xml
    <iron-ajax id="ajaxSearch" auto
        url="https://www.googleapis.com/youtube/v3/search"  
        params= "{{getCriteria()}}"  
        handleerror="handleError"
        handle-as="json"
        last-response="{{ajaxResponse}}">
    </iron-ajax>
```

```javascript
    getCriteria() {
        return {
                 "part": "snippet",
                  "q": this.search,
                  "key": "AIzaSyAuecFZ9xJXbGDkQYWBmYrtzOGJD-iDIgI",
                  "type": "video"
       };
    }
```

### Implement paper-search-panel

```xml
    <paper-search-panel
        placeholder="Search for anything..."
        hide-filter-button="[[hideFilterButton]]"
        search="{{search}}"
        count="{{count}}"          
        has-more="[[hasMore]]"
        loading="[[loading]]"
        filters="[[filters]]"     
        selected-filters="{{selectedFilters}}"
        on-change-request-params="loadData" >
```

### store favorites into local storage

```xml
    <iron-localstorage 
        id="YouTubeSearch" 
        name="my-app-storage"     
        value="{{favorites}}" 
        on-iron-localstorage-load-empty="initializeDefaults">
    </iron-localstorage>.
```
```javascript
            saveVideo(e) {
                if (!this.favorites.items) {
                    this.favorites.items = [];
                }
                this.favorites.items.push(e.model.item);
                this.set('favorites.count', this.favorites.items.length);
                this.set('favorites.items', this.favorites.items);
            }
```

## BUGS

Search Page

* Check duplicates (Thanks Ali :)
* Inititial search parameter
* search panel filter doesn't work. 
* paging is not impemented
* UI 

Favorites Page
* Remove function is not implemented  
* Page needs to refresh, afer new favorites added.

## TODO :

* use paper-panel filters.
* Implement social login 
* Save favorites into Firebase.
* Convert detail item to component 
* UI Refactoring

### Test

Chrome 63 (canary)
Chrom 60
Samsung Galaxy Note 4
Samsubg Galaxy Tab S2