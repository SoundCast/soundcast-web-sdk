# SoundCast Web SDK
SoundCast Web SDK is a javascript library for loading SoundCast audio ads in publishers websites.

## Table of Contents

* [Installation](#installation)
* [Initialize](#initialize)
* [Request Ad](#request-ad)
* [IOS specific](#ios-specific)
* [Event Listeners](#event-listeners)
* [Testing](#testing)

## Installation

The SoundCast Loader is a cache busted JS file who load the latest version of the SoundCast SDK.

A call method is triggered when the SoundCast SDK is ready.

In addition to integrate the SoundCast Loader, add the following code to your <head> tag

```
<script type="text/javascript">
(function(){
    var e = document.getElementsByTagName("script")[0];
    var script = document.createElement("script");
    script.src = "https://sdk.soundcast.fm/loader.min.js?cb=" + Date.now();
    script.async = true;
    script.defer = true;
    script.onload = function() {
      soundcastLoader.load(onLoad)
    };
    e.parentNode.insertBefore(script, e);
})();
</script>
```

## Initialize

Place this code before `</body>` tag in your web page to initialize the `SoundCast Audio Ad Manager`.

```
var onLoad = function() {
    var audioAdManager = new soundcast.AudioAdManager(document.getElementById('companionAdContainer'))
}
```

You can add a companion ad by linking the element where you want to place the companion ad (`companionAdContainer` in our example).

## Request Ad

Call this method to request for an audio ad.

```
audioAdManager.requestAd({ soundcastId: '[YOUR_SOUNDCAST_ID]', timeout: 5, autoplay: false })
```

Don't forgot to replace parameters between `[ ]` with your own IDs provided by us.

## Play Ad

Call this method to start playing the audio ad

```
audioAdManager.startAudioAd()
```

When the advertisement is over, the `soundcast.AdEvent.COMPLETE` will be fired. See the section [Event Listeners](#event-listeners) for more informations

## IOS specific

Due to iOS limitation, after user click on the play button you need to (without any delay):
- play your audio content
- pause your audio content
- play the soundcast audio ad

```
<button class="btn--start">play</button>
<audio class="player__audio" src="audio.mp3" type="audio/mp3"></audio>
<script>
document.querySelector('.btn--start').addEventListener('click', () => {
  document.body.querySelector('.player__audio').play()
  document.body.querySelector('.player__audio').pause()

  audioAdManager.startAudioAd()
})
</script>
```

## Event Listeners

You can add event listeners to follow ad completion.

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

## Testing

To verify that your integration is working properly, add the `testMode: true`  parameter to `requestAd` config
