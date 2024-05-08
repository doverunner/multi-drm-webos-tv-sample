# PallyCon Multi-DRM + webOS TV

> Multi-DRM integration sample for LG webOS TV application



## Overview

This document explains how to play `PallyCon Multi-DRM` content on webOS TV via `Shaka Player`.



## Supported Environments

- webOS TV 5.0 and later
- The sample in this document was tested on [LG  32SR85U](https://www.lg.com/us/monitors/lg-32sr85u-w-smart-monitor)(webOS 23).



## Checklist

- The emulator does not support DRM, so you must have a physical TV device.
- [webOS Studio Installation](https://webostv.developer.lge.com/develop/tools/webos-studio-installation)
- [App Testing with Developer Mode App](https://webostv.developer.lge.com/develop/getting-started/developer-mode-app#app-testing-with-developer-mode-app)


> You can see a more detailed development flow in webOS TV [Developer Workflow](https://webostv.developer.lge.com/develop/getting-started/developer-workflow).



## PallyConWebOS HTMLShaka Sample

> Shaka Player is an [Google open-source JavaScript library](https://github.com/shaka-project/shaka-player) for adaptive media. It plays adaptive media formats (such as [DASH](http://dashif.org/), [HLS](https://developer.apple.com/streaming/) and [MSS](https://learn.microsoft.com/en-us/iis/media/smooth-streaming/smooth-streaming-transport-protocol)) in a browser, without using plugins or Flash. Instead, Shaka Player uses the open web standards [MediaSource Extensions](https://www.w3.org/TR/media-source/) and [Encrypted Media Extensions](https://www.w3.org/TR/encrypted-media/).

#### The `PallyConTizen-HTMLShaka` sample uses Shaka Player. 

- Add the `Shaka Player` Javascript library.

  ```html
  <!-- index.html -->
  <head>
  	// shaka Player
  	<script src="shaka-player-4.8.0/shaka-player.compiled.debug.js" charset="utf-8"></script>
  </head>
  ```

- In the `index.html` file `startPlayer()` function, enter the `PallyCon Multi-DRM` licence server address in the `player.configure` value.

  ```javascript
  // index.html
  player.configure({
  	drm: {
  		// PallyCon License Request URL
  		servers: {
  			"com.widevine.alpha": "https://license-global.pallycon.com/ri/licenseManager.do" 
      }
  		//servers: { 
      //	"com.microsoft.playready": "https://license-global.pallycon.com/ri/licenseManager.do"
  		//}
  	}
  });
  ```

- Set the licence acquisition token in the `startPlayer()` function of the `index.html` file.

  ```javascript
  // index.html
  player.getNetworkingEngine().registerRequestFilter(function(type, request) {
  	if (type == shaka.net.NetworkingEngine.RequestType.LICENSE) {
  		// http header(custom data)
  		request.headers["pallycon-customdata-v2"] = "PallyCon Multi-DRM License Request Token";
  	}
  });
  ```



## More..

- [App Debugging](https://webostv.developer.lge.com/develop/getting-started/app-debugging)

- [Streaming Protocol and DRM](https://webostv.developer.lge.com/develop/specifications/streaming-protocol-drm)

- [webOS TV App Sample](https://webostv.developer.lge.com/develop/samples)




