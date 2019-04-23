# SimpleBrowser-Electron
Adds a simple using electron that allows you to browse the internet or view local html files with tabs and webviews.

![Chromel like demo](https://raw.githubusercontent.com/ohheyitskartik/SimpleBrowser-Electron/master/previews/in-action.gif)
*More previews at the end of readme file.

# Install
To install the package use the following code in the project directory.
``` 
npm i electron-navigation 
```

# Themes 
Themes
You can apply themes by downloading the ones on github and putting them in your <head> tag.
EXAMPLE: index.html
```
  
<head>
  <!-- your code here -->
    
  <link rel="stylesheet" href="relative/location/of/theme.css">
</head>

```

The themes folder also has a template theming file that you can use to style the tabs and controls exactly how you wish.
FILE: theme-template.css

```

/* back button, grouped in: .nav-icons */
#nav-ctrls-back {
    /* fill:#000; width:24px; height:24px; */
}


/* back button with no history, grouped in: .nav-icons.disabled */
#nav-ctrls-back.disabled {
    /* pointer-events:none; opacity:0.5; */
}
```

You can control how and if some elements are displayed by passing an options object through the main electron-navigation object.
```

const enav = new (require('electron-navigation')( { HERE } );
{ showBackButton : <boolean> }
//Shows/hides the back button in #nav-body-ctrls. Defaults to true.

{ showForwardButton : <boolean> }
//Shows/hides the forward button in #nav-body-ctrls. Defaults to true.

{ showReloadButton : <boolean> }
//Shows/hides the reload button in #nav-body-ctrls. Defaults to true.

{ showUrlBar : <boolean> }
//Shows/hides the url input in #nav-body-ctrls. Defaults to true.

{ showAddTabButton : <boolean> }
//Shows/hides the add button in #nav-body-tabs. Defaults to true.

{ closableTabs : <boolean> }
//Shows/hides the close button on tabs in .nav-tabs-tab. Defaults to true.

{ verticalTabs : <boolean> }
//Changes the direction tabs are stacked in #nav-body-tabs. Defaults to false.

{ defaultFavicons : <boolean> }
//Uses the default favicons instead of the unified color coded ones in .nav-tabs-tab. Defaults to false.

{ newTabCallback : <function> }
//Before a tab is created, an optional callback is invoked with (url, options). It can be set for the ElectronNavigation instance or passed inside newTab() as an option.
```

Optionally, the url and options can be altered and returned inside the callback result. The callback may define a postTabOpenCallback, which will receive the created webview.

If a falsy value is returned, the tab will not be created.

```
// Simple callbacks which does not alter the parameters
(url, options) => {
    return true;
}

// Prevent tab creation
(url, options) => {
    return false;
}

// Callback which redirects the opened tab
// Altered parameters imply that the tab should be shown
(url, options) => {
    url = "about:blank";
    return {url};
}

// Invoke callback after webview creation
(url, options) => {
    options.postTabOpenCallback = webview => {
        console.info("New webview created: ", webview);
    }
    return {options};
}
{ newTabParams : <function|array> }
//Parameters to pass to newTab() when a new tab is opened by the new tab button. The parameters may be an array or a function that returns an array. Defauls to ['http://www.google.com/', { close: options.closableTabs, icon: NAV.TAB_ICON }].

{ changeTabCallback : <function> }
//Function to invoke with visible webview after a new tab has become visible.

// all options and their default values if omitted.
let options = {
    showBackButton: true,
    showForwardButton: true,
    showReloadButton: true,
    showUrlBar: true,
    showAddTabButton: true,
    closableTabs: true,
    verticalTabs: false,
    defaultFavicons: false,
    newTabCallback: null
}
```
EXAMPLE : index.html
```
<script>    
    // the order doesn't matter    
    const enav = new (require('electron-navgation')) ({
        showAddTabButton: false,
        showUrlBar: true,
        showReloadButton: false
    });    
</script>
```
![demo2](https://raw.githubusercontent.com/ohheyitskartik/SimpleBrowser-Electron/master/previews/light-theme.PNG)

![demo3](https://raw.githubusercontent.com/ohheyitskartik/SimpleBrowser-Electron/master/previews/chrome-theme.png)
