<!--
author:   Andre Dietrich
email:    andre.dietrich@ovgu.de
version:  0.1.0
language: en
narrator: US English Female

comment:  Template for integrating 360 degree panorama images with the help of
          pannellum.

link:     https://pannellum.org/css/style.css
          https://cdn.pannellum.org/2.4/pannellum.css
          https://vjs.zencdn.net/7.1.0/video-js.css

script:   https://cdn.pannellum.org/2.4/pannellum.js
          https://vjs.zencdn.net/7.1.0/video.js
          https://pannellum.org/js/videojs-pannellum-plugin.js

@panorama
<div id="panorama_@0" style="width: 100%; height: 400px;"></div>

<script>
  pannellum.viewer('panorama_@0', {
        "type": "equirectangular",
        "panorama": "@1",
        "autoLoad": true,
        "hotSpots": [@2]
  });
</script>
@end


@panorama.hotspots
<div id="panorama_@0" style="width: 100%; height: 400px;"></div>

<script>
  pannellum.viewer('panorama_@0', {
        "type": "equirectangular",
        "panorama": "@1",
        "hotSpotDebug": true,
        "autoLoad": true,
        "hotSpots": []
  });
</script>
@end


@panorama.video
<video id="@0" class="video-js vjs-default-skin vjs-big-play-centered"
  controls preload="none" style="width:100%;height:400px;"
  crossorigin="anonymous">
  <source src="@1" type="video/mp4" />
    <p class="vjs-no-js">
        To view this video please enable JavaScript, and consider upgrading to
        a web browser that <a href="http://videojs.com/html5-video-support/"
        target="_blank">supports HTML5 video</a>
    </p>
</video>

<script>
videojs('@0', {
    plugins: {
        pannellum: {}
    }
});
</script>

@end


-->

# pannellum_template

A template for including pannellum 360 degree panorama images into
[LiaScript](https://liascript.github.io) courses. See the following links for
further information and documentation:


* See the pannellum docs [here...](https://pannellum.org)
* See the Github version of this document
  [here...](https://github.com/liaScript/pannellum_template)
* See the LiaScript version of this document
  [here...](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/pannellum_template/master/README.md)

## Images

Use the following macro to autoload a panorama image. The first parameter is a
simple id, that has to be used to distingush

* param1: a simple id that has to be used to distingush between multiple
  elements on one slide
* param2: url of the image, relative images are also ok
* param3: a set of hotspot parameters, see the following slide

@panorama(simple image,https://pannellum.org/images/cerro-toco-0.jpg,{})


### Images with hotSpots

The representation below, is just a Markdown user-friendly macro call. Just put
your macro in backtics so that the settings are nicely rendered on github. All
the code below the macro is simply passed as a third multiline parameter to the
macro above.

```json
@panorama(json_example,https://pannellum.org/images/bma-1.jpg)

{
    "pitch": 14.1,
    "yaw": 1.5,
    "type": "info",
    "text": "Baltimore Museum of Art",
    "URL": "https://artbma.org/"
},
{
    "pitch": -9.4,
    "yaw": 222.6,
    "type": "info",
    "text": "Art Museum Drive"
},
{
    "pitch": -0.9,
    "yaw": 144.4,
    "type": "info",
    "text": "North Charles Street"
}
```


### Identifying hotSpots

Use the following macro to print the coordinates of mouse clicks to the
browser's developer console, which makes it much easier to figure out where to
place hot spots.

`@panorama.hotspots(hotSpots,https://pannellum.org/images/cerro-toco-0.jpg)`

@panorama.hotspots(hotSpots,https://pannellum.org/images/cerro-toco-0.jpg)


## Videos

`@panorama.video(vidTest,https://pannellum.org/images/video/jfk.mp4)`

@panorama.video(vidTest,https://pannellum.org/images/video/jfk.mp4)
