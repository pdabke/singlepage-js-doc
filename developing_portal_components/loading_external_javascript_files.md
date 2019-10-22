# Loading External Javascript Files
Sometimes you need to load Javascript libraries that are specific to your component. SinglePage enables this via loadScript method on $app object that is available to all components loaded by SinglePage. Using this method ensures that the component-specific Javascript files are requested only when that component is used in the application. It also loads each file exactly once.

You should call the loadScript method in the mounted hook in your component. The following code shows how it is done in the built-in sp-twitter-feed component.
```javascript
  mounted: function () {
    var scriptLoaded = this.$app.loadScript('/sp-files/client/js/linkify.min.js',
    /* Callback function - called in case the script is not already loaded 
       Note that we bind to the component so that we can call 
       this.loadTweets later
     */
    function(event) { this.loadTweets(); }.bind(this));
    /* If loadScript returns true, call loadTweets right away */
    if (scriptLoaded) this.loadTweets();
  }
```
The method call return true if the file is already loaded. In that case you can proceed with your application logic that depend on that file. If the file is not loaded, your callback will be called once the file is loaded. Our twitter feed component needs linkify.min.js to convert URLs found in tweets to clickable links. In the code shown above, we call loadTweets immediately if the loadScript call returns true. If not, the same function is called when we receive the callback.