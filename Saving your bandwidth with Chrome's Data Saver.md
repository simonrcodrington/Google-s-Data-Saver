


#Saving your bandwidth with Chrome's Data Saver

You'd think that with the growing importance of mobiles that developers would be catering to them, creating awesome low bandwidth sites that load quickly when you're out and about. 

Overall though, you'd be wrong. Each year the average page weight / number of resources has increased, and along with all of the fancy animations, scrolling elements and other pretty things comes a slower web experience. 

If you want to both speed up your browsing experience and reduce how much you download, it might be worth looking into [Chrome's Data Saver option.](https://developer.chrome.com/multidevice/data-compression)

##Introducing Data Saver
Data Saver is a new feature for Chrome that works to significantly reduce mobile data usage. 

Starting way back in 2014, Chrome's developers worked on an experimental way to automatically reduce the total weight of pages by leveraging their own servers and technology. It's actually fairly similar to what [Opera has been offering for some time with their 'turbo' implementation.](http://www.opera.com/turbo) 


###How does it work?

At it's essence, Data Saver works by pushing the work of getting your web content to Google's servers instead of your device.

When you send off a request to load your favorite site, instead of your browser downloading your content, Data Saver will connect with one of Google's Optimization servers in their data center and provide the optimised content on your behalf. Here's a quick illustration. 

![enter image description here](https://lh3.googleusercontent.com/-oPuQODTmvsk/Vu6AQRkB97I/AAAAAAAAuSg/JBPCSSFetMUthWSXl3Q928fl-z3_hBjaA/s0/data_saver_overview.jpg "data_saver_overview.jpg")


###What does Data Saver actually do?

There are several steps to the optimization process that Google uses to serve up faster, more awesome content. 

**Content via HTTP2** 

Where it's possible the optimization servers request the content via HTTP/2 instead of HTTP.  HTTP/2 is a supercharged version of HTTP. Instead of having dozens of connections there is just one co-ordinated TCP connection, cutting down on the server back-and-forth traditionally associated with HTTP.  In addition HTTP/2 can cache future resources so that they can be instantly loaded when needed.

For a full breakdown you should have a [read of the HTTP/2 FAQ page](https://http2.github.io/faq/). If you're not too interested, just know that using HTTP2 is great and helps get you your content faster.

**Automatic conversion of images** 
One of the slowest components to download are images and rich media. Sometimes a single image can weight more than dozens of scripts / styles. 

With Data Saver, the optimization server performs an automatic conversion to the new [WebP format](https://developers.google.com/speed/webp/). WebP is a new image format that supports both **lossless**  (like PNG) and **lossey** (like JPG) formats.  The automatic conversion to WebP [saves an impressive amount of space](https://developers.google.com/speed/webp/); On average lossless images such as PNG's when converted became 25% smaller and lossey images such as JPG's where up to 34% smaller. 

You'd think the quality would reflect the size, but the differences between them were marginal. [Feel free to take a look at a comparison](https://developers.google.com/speed/webp/gallery). 

**No images shown at all**
For slower connections, instead of optimizing your images Google will opt to send you no images at all. Once the page has loaded it will prompt you with an option to enable images (which it will then fetch, compress and send down to the browser).

There's no way to force this by default, so if you're on a decent 3G connection or even 4G there is no option to automatically opt to do this (it's up to Google's discretion it seems). 

**Minification and compression**
Another part of the optimization process is that all resources will be automatically minified. 

Google's server will go through all of the CSS, JS and HTML content and automatically remove all the whitespace to cut down on size.  It also ensures that all content is served with gzip compression (further speeding up the process). 

**Better DNS requests**
When your device requests a site, often it will have to do a DNS lookup (to convert the URL to an IP address). As part of the compression process, Google's server will perform the DNS request and either get the information it needs from its cache or fetch it directly.  

This might seem like a small enhancement, but this does help to reduce name resolution and speed the whole process up.

**Privacy and secured traffic** 
On a quote note, **Data saver will only work with standard HTTP traffic**. As soon as you want to load an secure page over HTTPS or if you are using Incognito Mode, Data Saver will switch itself off and be processed like usual. 


###Enabling Data Saver

Data Saver was introduced for Mobile Chrome in December so there's a very good chance that your mobile chrome (on both Android and iOS) can enable this setting easily. Open up Chrome and go to 'Settings' and then 'Data Saver'. It's that easily to get started. 

If you're using the desktop version of Chrome you can enable this by download the [Data Saver Chrome Extension](https://chrome.google.com/webstore/detail/data-saver/pfmgfdlgomnbgkofeojodiodmgpgmkac).  It's an official extension from Google and once you have it up and running you should get a nifty data graph showing you how much data you've saved.

![enter image description here](https://lh3.googleusercontent.com/-01BgE1KvWTM/VwufWvR57nI/AAAAAAAAu6o/waMPdmqIIRA_iAArl0sOpWktuUaP8Y9cw/s0/data_saver_current.jpg "data_saver_current.jpg")

You can use this graph to see at a glace how much bandwidth you've saved. In addition you can click on the 'Details' page to see a detailed analysis of which saved yielded the best results 

![enter image description here](https://lh3.googleusercontent.com/-AJOKVS3OkSQ/VwugFZNQKvI/AAAAAAAAu68/ZNpkcrwSi-I7d16rAsFC1mN2Dn6SWw7Iw/s0/data_usage_breakdown.jpg "data_usage_breakdown.jpg")


##Data Saver in the real world
Now that you have a handle on what exactly Data Saver does, lets look at what exactly happens when you compare some websites side to side with this enabled. 

What we're interested in is the total size of the site, it's response time and if anything breaks along the way (since there is automatic compression involved). 

Each site was loaded several times and a fair average chosen (as most of these sites have advertising each page load will be subtly different). We're interested in the average speed and weight of the sites with and without Data Saver (when caching has been disabled).

###SitePoint - sitepoint.com
There's no better place to start than home. Looking at the SitePoint website it consists heavily of JS files and small images. 

**Data Saver Disabled**
![enter image description here](https://lh3.googleusercontent.com/-9nSbqHm2BGs/VwuZ1tzhaFI/AAAAAAAAu48/cOl5PHmAil0dnrwm8AsrlHAQKnZyomo6Q/s0/sitepoint_disabled_datasaver.jpg "sitepoint_disabled_datasaver.jpg")

The site ends up weighing in at about 1.2MB with 133 requests. It takes on average around 3 seconds to load. 

**Data Saver Enabled**
![enter image description here](https://lh3.googleusercontent.com/-VKum9K2kKrg/VwubFddsCuI/AAAAAAAAu5U/U0sI2ZQJWiUX3OOhqh1oRLOWWO4SsZMDQ/s0/sitepoint_datasaver_enabled.jpg "sitepoint_datasaver_enabled.jpg")

After Data Saver has been enabled the page weight drops to around 700KB - 780KB. The number of requests stays consistent, however the page takes a solid 1 second longer to load. 

The reduction here was mainly from minifying JS / HTML resources. Data Saver ended saved us a good portion of bandwidth with only a slight delay.

###Web Bird Digital - web.bird.digital
Always good to compare potential savings on your own websites. This site is more media heavy with several portfolio images, a large slider and smaller thumbnails. 

**Data Saver Disabled**

![enter image description here](https://lh3.googleusercontent.com/-G2XF0OZPal0/VwuW0XCQvQI/AAAAAAAAu4E/VnPXAQvYkxwYbD1w8dk3TNKp5Pw5PcjmA/s0/webbird_datasaver_disabled.jpg "webbird_datasaver_disabled.jpg")

There's around 1.2MB of data being downloaded across 63 requests. The load time finishes in around 1.8 - 2 seconds.

**Data Saver Enabled**
![enter image description here](https://lh3.googleusercontent.com/-vRuAzeF-Muw/VwuW5cFItyI/AAAAAAAAu4U/nhH2GDivEGUH03vHbd8NMqTI5Bq2VIZIw/s0/webbird_datasaver_enabled.jpg "webbird_datasaver_enabled.jpg")

When Data Saver is enabled the size drops drastically, down to around 650KB - 700KB. The reduction in size comes almost entirely from the dynamic conversion of images to the WebP format. The tradeoff for this data saver is the download speed, taking on average around another 0.5 seconds to download. 

###eBay - ebay.com

One of everyone favorite auction sites. eBay's homepage (when not logged in) showcases several of the days latest deals along with a somewhat random collection of products, categorized into actions.  It's another media heavy site. 

**Data Saver Disabled**
![enter image description here](https://lh3.googleusercontent.com/-Wl4D6gVbHfw/VwudIxqW3zI/AAAAAAAAu5s/sALsd9ka0zAXd_FaDXQ6sWp0cgDy_MWeQ/s0/ebay_datasaver_disabled.jpg "ebay_datasaver_disabled.jpg")

The site weighs in at about 2.4MB with 200 requests. All of this takes about 4.5 seconds to fully load. 

**Data Saver Enabled**
![enter image description here](https://lh3.googleusercontent.com/-DzeEd7FhL78/VwudsRm5nFI/AAAAAAAAu6M/CGBuuW2cnzQd6YHrWQFymKt8-sPeGoiog/s0/ebay_datasaver_enabled.jpg "ebay_datasaver_enabled.jpg")


When Data Saver is enabled the page weight drops sharply, down to just 1.4MB. Generally Data Saver makes pages loader slower as it has to push everything through Google's servers. However, for eBay it seems to remain about the same (and sometimes was actually faster). 

This is a really good case where we've almost halved the download size and took nothing as a trade-off




###Wrapping it all up
Overall Data Saver is an awesome useful feature that could potentially help everyone cut down on their mobile data usage. 

We've looked at how this works with a couple of sample sites. Generally we end up dropping a good 30% - 40% of the total page weight with very negligible speed decreases / visual clarify.  

As with everything it has it's drawbacks. Since data saver is compressing you potentially sacrifice quality and speed in exchange for lower download sizes. Also worthy of mention is in using Data Save you rely on a third party company (Google) to honor your privacy and data. 

After all is said and done you will need to play around with Data Saver to see if it's right for you.