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

    <iron-ajax id="ajaxSearch" auto
        url="https://www.googleapis.com/youtube/v3/search"  
        params= "{{getCriteria()}}"  
        handleerror="handleError"
        handle-as="json"
        last-response="{{ajaxResponse}}">
    </iron-ajax>

### Implement paper-search-panel

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

### store favorites into local storage

    <iron-localstorage 
        id="YouTubeSearch" 
        name="my-app-storage"     
        value="{{favorites}}" 
        on-iron-localstorage-load-empty="initializeDefaults">
    </iron-localstorage>.

## TODO :

* use paper-panel filters.
* Implement social login 
* Save favorites into Firebase.
* Convert detail item to component 

