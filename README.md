# Assignment Summer School Polymer 2017 (ITAC0249)

![ING Summer School](/docs/1.png)

## Template : 

Polymer Starter Kit

## Components 

* iron-ajax
* paper-search-panel
* iron-localstorage
* paper-button
* paper-toast

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
### Paper toast

```css
        #toastWarning {
              --paper-toast-background-color: red;
              --paper-toast-color: white;
        } 
        #toastOk {
              --paper-toast-background-color: blue;
              --paper-toast-color: white;
        }
```

```xml
    <paper-toast id="toastOk" text=""></paper-toast>
    <paper-toast id="toastWarning" text=""></paper-toast>
```
```javascript
        this.$.toastOk.text = e.model.item.snippet.title + " added into favorites!";
        this.$.toastOk.open();

        this.$.toastWarning.text = e.model.item.snippet.title + " is already added into favorites!";
        this.$.toastWarning.open();
```

## BUGS

Search Page

- [x] Check duplicates (Thanks Ali :)  
- [x] Inititial search parameter  
- [ ]  search panel filter doesn't work. 
- [ ]  paging is not impemented
- [ ] toast messages display behind navigation bar.
- [ ] UI 

Favorites Page
- [x] Remove function is not implemented   
- [ ] Page needs to refresh, afer new favorites added.

## TODO :

- [ ] use paper-panel filters.
- [ ]  Implement social login 
- [ ]  Save favorites into Firebase.
- [ ]  Convert detail item to component 
- [ ]  UI Refactoring
- [ ]  Unit test

 

### Test

- [x] Chrome 63 (canary)
- [x] Chrom 60
- [x] Samsung Galaxy Note 4
- [x] Samsubg Galaxy Tab S2