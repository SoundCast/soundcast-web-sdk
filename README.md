# SoundCast Web SDK
SoundCast Web SDK is a javascript library for loading SoundCast audio ads in publishers websites.

## Table of Contents

* [Installation](#installation)
* [Initialize](#initialize)
* [Event Listeners](#event-listeners)
* [Request Ad](#request-ad)
* [IOS specific](#ios-specific)
* [Testing](#testing)

## Installation

Place this code before `</head>` tag in your web page to load `SoundCast Web SDK`.

```
<!-- SoundCast SDK -->
<script src="https://sdk.soundcast.fm/loader.js"></script>
<!-- /SoundCast SDK -->
```

## Initialize

Place this code before `</body>` tag in your web page to initialize the `SoundCast Audio Ad Manager`.

```
const sdkReady = function() {
    var audioAdManager = new soundcast.AudioAdManager(document.getElementById('companionAdContainer'));
}
loadJS('https://sdk.soundcast.fm/library.min.js', sdkReady, document.body);
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
audioAdManager.requestAd({soundcastId: [YOUR_SOUNDCAST_ID], timeout: 5});
```

Don't forgot to replace parameters between `[ ]` with your own IDs provided by us.

## IOS specific
Due to IOS limitation, the ad needs to be stiched to the content. In order to do so, you just need to add the following function to your script.

```

  function stichAd4Ios(playerClassName, soundcastId, testMode=false) {
    var src = document.body.querySelector(playerClassName).src;
      var pageUrl = window.location;
      var pageUrl = window.location;
      src = 'https://stitch.api.soundcast.fm/v1/podcast?podcastUrl='+src;
      src =  src + '&soundcastId='+soundcastId;
      src =  src + '&pageUrl='+pageUrl;
      if(testMode) {
        src =  src + '&test=true';
      }
      document.body.querySelector(playerClassName).src = src;
  }

```

And when you call the Ad, you call the Ad sitching only for for IOS.

```
    var testMode = false;
    var soundcastId
    var _iOSDevice = !!navigator.platform.match(/iPhone|iPod|iPad/);
     if (_iOSDevice) {
        stichAd4Ios('.player__audio', soundcastId, testMode);
        document.body.querySelector('.player__audio').play();
        playing = true;
      } else { // Web + Android
        document.body.querySelector('.player__audio').play();
        playing = true;
        pauseAudioContent();
        audioAdManager.requestAd({soundcastId: soundcastId, testMode: testMode, timeout: 5});
      }
```


## Integration Sample 

https://demo.soundcast.fm/

## Testing

To verify that your integration is working properly, add the `testMode` parameter to `loadAd` config

## Any questions

Please contact our support team.
