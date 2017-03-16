# Polymer UI Extensions

Idea:

Define polymer code snippets which can be used in the generic UI.

In a SkysailServerResource implementation add something like:

```
public List<String> getPolymerUiExtensions() {
    return Arrays.asList("sky-left-nav");
}
```

Example polymer file:

Please note the naming convention: sky-left-nav becomes 

/&lt;appname&gt;/v1/sky-&lt;appname&gt;/sky-left-nav.html

```
<link rel="import" href="/_polymer/bower_components/polymer/polymer.html">

<dom-module id="sky-spotify-left-nav">
  <template>

    <a href='/spotify/v1/me'>me</a><br>
    <a href='/spotify/v1/me/playlists'>playlists</a><br>

    <iron-ajax
        auto
        url="http://localhost:2021/spotify/v1/me/playlists"
        handle-as="json"
        on-response="handleResponse"
        debounce-duration="300"></iron-ajax>

    <ul>    
    <template as="playlist" is="dom-repeat" items="{{payload.items}}">
      <li><a href='{{openSpotify(playlist)}}' target="_spotify">{{playlist.name}}</a></li>
    </template>
    </ul>

    <content></content>    
  </template>

  <script>
    Polymer({

      is: 'sky-spotify-left-nav',

      properties: {
          payload: { type: Object, value: [] }
      },
      handleResponse: function(request) {
          console.log(request.detail.response.payload);
          this.payload = JSON.parse(request.detail.response.payload);
          console.log(this.payload);
      },
      openSpotify: function(playlist) {
          return playlist.external_urls['spotify'];
      }
    });
  </script>
</dom-module>
```

Testing in bundle skysail.app.spotify, skysail.app.website

In StringTemplateRenderer constructor, this is saved to uiPolymerExtensions, a list of Strings, which is read in bst\_head like this:

```
<!-- UI Extensions from bundles (if any) -->
$converter.uiPolymerExtensions: {extension | <link rel="import" href="$extension$">};separator="\n"$
```



