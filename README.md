README
------

This is a public feed aggregator. 
Thanks to Twitter, things are a little more complicated.

Supported platforms:

1.  Facebook Pages
    Provide the link to a Page's RSS feed. You can find this by
    a) logging into Facebook
    b) go to the page - in the left column, choose "Subscribe via RSS" and copy the resulting URL.
2.  RSS/Atom feeds
    Provide the link to the feed.
3.  Twitter
    Just provide the Twitter screenname. We use Twitter's REST API instead of YQL due to Twitter's [recent discontinuation of RSS].

The key option is feeds. Pass a JSON list, where each object has 3 fields:

1.  title: Pick a descriptive title
2.  type: 'rss', 'facebook', or 'twitter'
3.  id: The *full URL* or an RSS/Atom feed, or a Twitter screenname

Example:

## 10-second setup

1.  Include JQuery, jquery.jsonp, and so.what.social somewhere in `<head>...</head>`

        <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js" type="text/javascript"></script>
        <script src="jquery.jsonp-2.1.4.js" type="text/javascript"></script>
        <script src="so.what.social.js" type="text/javascript"></script>

2.  Include an empty div somewhere in `<body></body>` that will be filled in by so.what.social
    It's nice to include some kind of "loading" animation so your users aren't *too* shocked when the plugin loads.
    
        <body>
        ...
        <div id="activityFeed">
            <img id="loading" src="ajax-loading.gif" />
        </div>
        ...
        </body>

3.  Call so.what.social and pass feeds to it, along with any options. This goes in `<head>...</head>`

        <script type="text/javascript">
            $(document).ready(function() {
                $("#activityFeed").soWhatSocial({
                    "feeds": [
                        {
                            "title": "Some awesome RSS or Atom feed",
                            "type": "rss",
                            "id": "https://blog.honestappalachia.org/feed/"
                        },
                        {
                            "title": "My favorite Twitter",
                            "type": "twitter",
                            "id": "rampswv"
                        },
                        {
                            "title": "Sweet Facebook, bro",
                            "type": "facebook",
                            "id": "http://www.facebook.com/feeds/page.php?id=135221739823874&format=rss20"
                        }
                    ],
                });
            });
        </script>

## TODO

1.  Incorporate more settings for easy customization without digging into the code.
    Ideas:
    1.  URLs for feed-type icons. Perhaps a dictionary that matches with "type"
    2.  Number of posts to show (total)
    3.  Max. posts from any source
2.  There's a lot of repetitive code in Facebook/RSS right now. Think about it.
3.  Make the grey link boxes clickable - should take you to the original asset.
    Depends on original resource type, will have to build a URL (see earlier URL work in feedeater,
    esp. for Twitter).
4.  Better error handling.
5.  The building of the <li> text (POST_ARRAY[COUNT][0]) is awkward and repetitive. Better way?

## Credit

My work on this plugin was inspired by John Patrick Given's excellent [So So Social Plugin]. The license
will be determined once I hear back from him.

[So So Social Plugin]: http://johnpatrickgiven.com/jquery/soSoSocial/
