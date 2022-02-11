<p align="center"><a href="https://rudderstack.com"><img src="https://user-images.githubusercontent.com/59817155/126267034-ae9870b7-9137-4f45-be65-d621b055a972.png" alt="RudderStack - Customer Data Platform for Developers" height="50"/></a></p>
<h1 align="center"> Candidate Assignment</h1>
<br/>

## Assignment

This assignment is aimed at evaluating your technical content writing expertise. Your objective is to go through the document and suggest changes to improve the clarity and brevity of the instructions.

These suggestions may involve adding/removing/modifying the instructions, restructuring the content, and any other changes that you see fit.

The end goal is to make it easier for the end-user to use the SDK by having your documentation as the reference point for any information they might need.

## Instructions

Add your suggestions, comments, and changes to standardize and improve the following document and raise a PR for our review.

----

# [](https://github.com/rudderlabs/rudder-sdk-js/blob/master/README.md#rudderstack-javascript-sdk)RudderStack JavaScript SDK

The RudderStack JavaScript SDK allows you to utilize our npm module `rudder-sdk-js` or `rudder-analytics.js` library to start sending event data from your website to RudderStack. You can then further transform and route this event data to the destination platform of your choice.

> For detailed documentation on the RudderStack JavaScript SDK, click [**here**](https://docs.rudderstack.com/stream-sources/rudderstack-sdk-integration-guides/rudderstack-javascript-sdk).
-----

This Quick Start Guide will help you get up and running with using the RudderStack JavaScript SDK in no time. You just need to follow the steps below:

## [](https://github.com/rudderlabs/rudder-sdk-js/blob/master/README.md#step-1-install-rudderstack-using-the-code-snippet)Step 1: Install RudderStack Using the Code Snippet

To integrate the SDK, place the following code snippet in the `<head>` section of your website.

You can use either the minified or non-minified version of the code.

### Minified code 

The minified version is as follows:

```
<script>
rudderanalytics=window.rudderanalytics=[];for(var methods=["load","page","track","identify","alias","group","ready","reset","getAnonymousId","setAnonymousId"],i=0;i<methods.length;i++){var method=methods[i];rudderanalytics[method]=function(a){return function(){rudderanalytics.push([a].concat(Array.prototype.slice.call(arguments)))}}(method)}rudderanalytics.load(YOUR_WRITE_KEY,DATA_PLANE_URL),rudderanalytics.page();
</script>

<script  src="https://cdn.rudderlabs.com/v1/rudder-analytics.min.js"></script>

```
### Non-minified Code

The non-minified version of the code is shown below:

```
<script>
	rudderanalytics = window.rudderanalytics = [];

	var  methods = [
		"load",
		"page",
		"track",
		"identify",
		"alias",
		"group",
		"ready",
		"reset",
		"getAnonymousId",
    		"setAnonymousId"
	];

	for (var i = 0; i < methods.length; i++) {
  		var method = methods[i];
  		rudderanalytics[method] = function (methodName) {
    			return function () {
      				rudderanalytics.push([methodName].concat(Array.prototype.slice.call(arguments)));
    			};
  			}(method);
	}
	rudderanalytics.load(YOUR_WRITE_KEY, DATA_PLANE_URL);
	//For example,
	//rudderanalytics.load("1Qb1F3jSWv0eKFBPZcrM7ypgjVo", "http://localhost:8080");
	rudderanalytics.page();
</script>

<script  src="https://cdn.rudderlabs.com/v1/rudder-analytics.min.js"></script>

```

You can also execute the min file in async/defer way, like:

```
<script async src="https://cdn.rudderlabs.com/rudder-analytics.min.js"></script>
```

Combining the initialization and the above async script together, we get:

```
    <script type="text/javascript">
    !function(){var e=window.rudderanalytics=window.rudderanalytics||[];e.methods=["load","page","track","identify","alias","group","ready","reset","getAnonymousId","setAnonymousId"],e.factory=function(t){return function(){var r=Array.prototype.slice.call(arguments);return r.unshift(t),e.push(r),e}};for(var t=0;t<e.methods.length;t++){var r=e.methods[t];e[r]=e.factory(r)}e.loadJS=function(e,t){var r=document.createElement("script");r.type="text/javascript",r.async=!0,r.src="https://cdn.rudderlabs.com/v1/rudder-analytics.min.js";var a=document.getElementsByTagName("script")[0];a.parentNode.insertBefore(r,a)},e.loadJS(),
    e.load(YOUR_WRITE_KEY,DATA_PLANE_URL),
    e.page()}();
    </script>
 ```

> **NOTE**: Whichever version of the code you use, you need to replace `YOUR_WRITE_KEY` with the write key in the RudderStack Control Plane and `DATA_PLANE_URL` with the data plane URL. <br><br>

### Write key and Data plane URL

- To get the source write key, follow [**this guide**](https://docs.rudderstack.com/get-started/installing-and-setting-up-rudderstack/sending-test-events#get-the-source-write-key).
- To get the data plane URL, follow [**this guide**](https://docs.rudderstack.com/get-started/installing-and-setting-up-rudderstack#what-is-a-data-plane-url-where-do-i-get-it).

> **NOTE** : In all the above versions, there is an explicit `page` call at the end. This is added to ensure that whenever the SDK loads in a page, a `page` call is being sent. You can remove this call completely or modify with extra page properties to suit your requirement. You can also add `page` calls in your application in places not tied directly to page load, ex: virtual page views, page renders on route change such as in SPAs.

| **IMPORTANT**: We are moving our SDK to a different path from [https://cdn.rudderlabs.com/rudder-analytics.min.js](https://cdn.rudderlabs.com/rudder-analytics.min.js) to [https://cdn.rudderlabs.com/v1/rudder-analytics.min.js](https://cdn.rudderlabs.com/v1/rudder-analytics.min.js). The earlier path may not be maintained in coming releases. |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Alternative Installation using NPM

While we recommended you use the JavaScript snippet above to use the SDK in your websites, you can also use this [NPM module](https://www.npmjs.com/package/rudder-sdk-js) to package RudderStack directly into your project.

- To install, run:
  `npm install rudder-sdk-js --save`
- Since the module exports a bunch of APIs on an already-defined object combined with node module caching, you should run the below code only once and use the exported object throughout your project :

```
import * as rudderanalytics from "rudder-sdk-js"
rudderanalytics.load(YOUR_WRITE_KEY, DATA_PLANE_URL)
rudderanalytics.ready(() => {console.log("we are all set!!!")})
export  {  rudderanalytics  }
```

For ES5, with _require_:

```
var rudderanalytics  =  require("rudder-sdk-js")
rudderanalytics.load(YOUR_WRITE_KEY, DATA_PLANE_URL)
exports.rudderanalytics  =  rudderanalytics
```

You can also refer to the sample projects for a walkthrough of the above: [Sample Angular Project](https://github.com/rudderlabs/rudder-analytics-angular) and [Sample React Project](https://github.com/rudderlabs/rudder-analytics-react)

**SDK-supported Browser Versions**

- Safari >=7
- IE >=10
- Edge >=15
- Mozilla >=40
- Chrome >= 37
- Opera >= 23
- Yandex>=14.12

> **NOTE**: If the SDK doesn't work on the versions you are targeting, check if adding browser polyfills to your application solves the issue.

### [](https://github.com/rudderlabs/rudder-sdk-js/blob/master/README.md#step-2-identify-your-users-using-the-identify-method)Step 2: Identify Your Users With the `identify()` Method:

The `identify()` method allows you to link users and their actions to a specific userid.

A sample example of how the `identify()` method works is as shown:

```
rudderanalytics.identify(
      "12345",
      { email: "name@domain.com" },
      {
        page: {
          path: "",
          referrer: "",
          search: "",
          title: "",
          url: ""
        }
      },
  () => {console.log("in identify call");}
);

```

In the above example, information such as the user ID, email along with contextual information such as IP address, anonymousId, etc. will be captured.

> **NOTE**: There is no need to call `identify()` for anonymous visitors to your website. Such visitors are automatically assigned an `anonymousId`.

### [](https://github.com/rudderlabs/rudder-sdk-js/blob/master/README.md#step-3-track-your-users-actions-using-the-track-method)Step 3: Track Your Users’ Actions With the `track()` Method

The `track()` method allows you to track any actions that your users might perform.

A sample example of how the `track()` method works is as shown:

```
rudderanalytics.track(
  "test track event GA3",
  {
    revenue:  30,
    currency:  'USD' ,
    user_actual_id:  12345
  },
  () => {console.log("in track call");}
);

```

In the above example, the method tracks the event ‘**test track event GA3**’, and information such as the revenue, currency, anonymousId.

You can use this method to track various other success metrics for your website, such as user signups, item purchases, article bookmarks, and much more.

> **NOTE**: To override contextual information, for ex: anonymizing IP and other contextual fields like page properties, the following template can be used. Similarly one can override the auto-generated anonymousId with provided ID. For this:

```
rudderanalytics.track(
  "test track event GA3",
  {
    revenue:  30,
    currency:  'USD' ,
    user_actual_id:  12345
  },
  () => {console.log("in track call");}
);
```

You’ve now successfully installed `rudder-analytics.js` tracking. You can enable and use any event destination to send your event data via RudderStack, in no time at all.

## Contact Us

For more support on using the RudderStack JavaScript SDK, feel free to [contact us](https://rudderstack.com/contact/) or start a conversation on our [Slack](https://resources.rudderstack.com/join-rudderstack-slack) channel.
