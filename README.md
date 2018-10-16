# SoundCast Web SDK
SoundCast Web SDK is a javascript library for loading SoundCast audio ads in publishers websites.

## Table of Contents

* [Installation](#installation)
* [Initialize](#initialize)
* [Event Listeners](#event-listeners)
* [Request Ad](#request-ad)
* [Testing](#testing)

## Installation

Place this code before `</head>` tag in your web page to load `SoundCast Web SDK`.

```
<!-- SoundCast SDK -->
<script src="https://sdk.soundcast.fm/library.min.js"></script>
<!-- /SoundCast SDK -->
```

## Initialize

Place this code before `</body>` tag in your web page to initialize the `SoundCast Audio Ad Manager`.

```
var audioAdManager = new soundcast.AudioAdManager(document.getElementById('companionAdContainer'));
```

You can add a companion ad by linking the element where you want to place the companion ad (`companionAdContainer` in our example).

## Event Listeners

Add event listeners to get feedback from the library.

```
audioAdManager.addEventListener(
    soundcast.AdEvent.[EVENT_NAME],
    [CALLBACK_METHOD],
    false
  );
```

`[EVENT_NAME]` is the name of the event you want to listen and `[CALLBACK_METHOD]` is fired when this event occurs.

Here is the full list of events :
* AD_ERROR: no ad or ad failed to load, start your audio content
* STARTED: ad started
* DURATION_CHANGE: ad duration change
* FIRST_QUARTILE: ad first quartile
* MIDPOINT: ad midpoint
* THIRD_QUARTILE: ad third quartile
* COMPLETE: ad complete, start your audio content

## Request Ad

Call this method to request for an audio ad.

```
audioAdManager.requestAd({networkId: [YOUR_NETWORK_ID], siteId: [YOUR_SITE_ID], tagId: [YOUR_TAG_ID], timeout: 5});
```

Don't forgot to replace parameters between `[ ]` with your own IDs provided by us.


## Testing

To verify that your integration is working properly, add the `testMode` parameter to `loadAd` config
