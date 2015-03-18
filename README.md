# docker-Manet
> There is only one true thing: instantly paint what you see. When you've got it, you've got it. When you haven't, you begin again. All the rest is humbug.
**docker-Manet** is the docker format of **Manet** REST API server which allows capturing screenshots of websites using various parameters. It is a good way to make sure that your websites are responsive or to make thumbnails.

**docker-Manet** could use  [PhantomJs](http://phantomjs.org) engines to work.
* **PhantomJS** runs on top of [WebKit](https://www.webkit.org) and [JavaScriptCore](http://trac.webkit.org/wiki/JavaScriptCore).
**docker-Manet** exposed port is 8891

## REST API

REST API is available on "<$your docker ip>:<$your docker port>/" using:

* GET method
* POST method with `Content-Type`:
    * *application/json*
    * or *application/x-www-form-urlencoded*

Few rules:

* The `"url"` parameter must be specified.
* Query parameters will be used in priority and override others.


### Query parameters

<dl>
  <dt>url</dt>
  <dd>Website address (URL). This is the only required parameter for the HTTP request. It is unnecessary for the most cases to configure scheme. Example: "github.com".</dd>

  <dt>width</dt>
  <dd>This property allows to change the width of the viewport, e.g., the size of the window where the webpage is displayed (default: 1024)</dd>

  <dt>height</dt>
  <dd>This property allows to change the height of the viewport. If width is defined and height is not defined, than full page will be captured.</dd>

  <dt>clipRect</dt>
  <dd>This property defines the rectangular area of the web page to be rasterized. Format: "top,left,width,height", example: "20,20,640,480".</dd>

  <dt>zoom</dt>
  <dd>Zoom factor of the webpage display. Setting a value to this property decreases or increases the size of the web page rendering. A value between 0 and 1 decreases the size of the page, and a value higher than 1 increases its size. 1 means no zoom (normal size). (default: 1).</dd>

  <dt>quality</dt>
  <dd>The compression quality. A number between 0 and 1 (default value: 1). Quality parameter doesn't work for PNG file format.</dd>

  <dt>delay</dt>
  <dd>Do a pause during the given amount of time (in milliseconds) after page opening (default: 100).</dd>

  <dt>format</dt>
  <dd>Indicate the file format for output image (default is "png"). Possible values: jpg, jpeg, png, gif, pdf</dd>

  <dt>agent</dt>
  <dd>String to define the "User-Agent" in HTTP requests. By default, it is something like:
    <ul>
        <li><b>PhantomJS:</b> Mozilla/5.0 (Macintosh; Intel Mac OS X) AppleWebKit/534.34 (KHTML, like Gecko) PhantomJS/1.9.0 (development) Safari/534.34</li>
        <li><b>SlimerJS:</b> Mozilla/5.0 (X11; Linux x86_64; rv:21.0) Gecko/20100101 SlimerJS/0.7</li>
    </ul>
  </dd>

  <dt>headers</dt>
  <dd>This property specifies additional HTTP request headers that will be sent to the server for every request issued (for pages and resources). Format: "key1=value1;key2=value2;..." Headers names and values get encoded in US-ASCII before being sent. Please note that setting the 'User-Agent' will overwrite the value set via "agent" parameter.</dd>

  <dt>user</dt>
  <dd>User name to give to HTTP Basic authentication.</dd>

  <dt>password</dt>
  <dd>Password to give to HTTP Basic authentication.</dd>

  <dt>js</dt>
  <dd>false to deactivate javascript in web pages (default is true).</dd>

  <dt>images</dt>
  <dd>false to deactivate the loading of images (default is true).</dd>

  <dt>force</dt>
  <dd>Use the force reloading of web page without using cache (default is false).</dd>

  <dt>callback</dt>
  <dd>Return an empty response immediately (HTTP 200 OK), then send a POST request to the callback URL when the screenshot is ready (with image in the body).</dd>

</dl>


### Query examples

For a quick test with the command line (using `curl`), type:

```bash
curl http://<$your docker ip>:<$your docker port>/?url=github.com > github.png
curl -H "Content-Type: application/json" -d '{"url":"github.com"}' http://<$your docker ip>:<$your docker port>/ > github.png
curl -H "Content-Type: application/x-www-form-urlencoded" -d 'url=github.com' http://<$your docker ip>:<$your docker port>/ > github.png
```

or (using `wget`)

```bash
wget http://<$your docker ip>:<$your docker port>/?url=github.com -O github.png
```

Here are some query examples that could be executed by any REST API client:

```
# Take a screenshot of the github.com.
GET /?url=github.com

# Custom viewport size. Return a 800x600 PNG screenshot of the github.com homepage.
GET /?url=github.com&width=800&height=600

# Clipping Rectangle. Return a screenshot clipped at [top=20, left=30, width=90, height=80]
GET /?url=github.com&clipRect=20%2C30%2C90%2C80

# Zoom rendered page in 2 times.
GET /?url=github.com&zoom=2

# Specify image output format.
GET /?url=github.com&format=jpeg

# Disable JavaScript. Return a screenshot with no JavaScript executed.
GET /?url=github.com&js=false

# Disable images. Return a screenshot without images.
GET /?url=github.com&images=false

# Custom User Agent.
GET /?url=github.com&agent=Mozilla%2F5.0+(X11%3B+Linux+x86_64)+AppleWebKit%2F537.36+(KHTML%2C+like+Gecko)+Chrome%2F34.0.1847.132+Safari%2F537.36

# HTTP Basic Authentication. Return a screenshot of a website requiring basic authentication.
GET /?url=mysite.com&user=john&password=smith

# Screenshot delay. Return a screenshot of the github.com homepage 1 second after it's loaded.
GET /?url=github.com&delay=1000

# Force page reloading. Return a screenshot without using file cache.
GET /?url=github.com&force=true

# Specify custom HTTP headers.
GET /?url=google.com&headers=User-Agent=Firefox;Accept-Charset=utf-8

# Asynchronous call.
GET /?url=github.com&callback=http://localhost:8891
```

## Sandbox UI

Sandbox UI is available on "/" by direct GET request without `"url"` query parameter.
It is a simple playground to build HTTP requests and try them.

Demo instance is available on [Heroku](https://heroku.com): [https://manet.herokuapp.com](https://manet.herokuapp.com/)

**docker-Manet** is prodly dockerized by  
[https://earlyclaim.com](https://earlyclaim.com) RESERVE YOUR FAVORITE USERNAME IN NEW STARTUPS
the man behind it is Walter Franchetti [https://twitter.com/frnwtr](@frnwtr)


