<!--
author:   Andre Dietrich
email:    andre.dietrich@ovgu.de
version:  0.1.1
language: en
narrator: US English Female

logo:     https://cdn.pixabay.com/photo/2010/12/14/11/44/forest-3147_960_720.jpg

comment:  Template for integrating 360 degree panorama images with the help of
          pannellum.

link:     https://pannellum.org/css/style.css
          https://cdn.pannellum.org/2.4/pannellum.css
          https://vjs.zencdn.net/7.1.0/video-js.css

script:   https://cdn.pannellum.org/2.4/pannellum.js
          https://vjs.zencdn.net/7.1.0/video.js
          https://pannellum.org/js/videojs-pannellum-plugin.js

@Pannellum.panorama: @Pannellum._panorama_(@uid,@0,{})
@Pannellum.panoramaWithHotspots: @Pannellum._panorama_(@uid,@0,```@1```)
@Pannellum.hotspots: @Pannellum._panorama_(@uid,@0, ,true)
@Pannellum._panorama_
<div id="panorama_@0" style="width: 100%; height: 400px;"></div>

<script>
  setTimeout(function(e) {
    let debug = "@3";
    pannellum.viewer('panorama_@0', {
          "type": "equirectangular",
          "hotSpotDebug": (debug == "true" ? true : false),
          "panorama": "@1",
          "autoLoad": true,
          "hotSpots": [@2]
    });
  }, 1000);
</script>
@end

@Pannellum.video
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
setTimeout(function(e) {
  videojs('@0', {
      plugins: {
          pannellum: {}
      }
  })}, 1000);
</script>

@end
-->

# Pannellum - Template

                         --{{0}}--
A template for including pannellum 360 degree panorama images into
[LiaScript](https://liascript.github.io) courses. See the following links for
further information and documentation:

                          {{0-1}}
* See the pannellum docs [here...](https://pannellum.org)
* See the Github version of this document
  [here...](https://github.com/liaTemplates/pannellum)
* See the LiaScript version of this document
  [here...](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaTemplates/pannellum/master/README.md)


                         --{{1}}--
There are three ways to use this template. The easiest way is to use the
`import` statement and the url of the raw text-file of the master branch or any
other branch or version. But you can also copy the required functionionality
directly into the header of your Markdown document, see therefor the
[last slide](#6). And of course, you could also clone this project and change
it, as you wish.

                           {{1}}
1. Load the macros via

   `import: https://raw.githubusercontent.com/liaTemplates/pannellum/master/README.md`

2. Copy the definitions into your Project

3. Clone this repository on GitHub


## `@Pannellum.panorama`

                         --{{0}}--
Simply call the macro `@Pannellum.panorama` with the url of the 3D image as the
only parameter (in parenthesis).

@Pannellum.panorama(https://pannellum.org/images/cerro-toco-0.jpg)

## `@Pannellum.panoramaWithHotspots`

                         --{{0}}--
Use `@Pannellum.panoramaWithHotspots`, the url of the 3D image and a JSON list
of hotspots. You can use the macro code-block notation for this, the content of
the is then block is passed as the second parameter. You can use the macro on
the next slide to identifier your points of interest.

```json @Pannellum.panoramaWithHotspots(https://pannellum.org/images/bma-1.jpg)
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

## `@Pannellum.hotspots`

                         --{{0}}--
If you use `@Pannellum.hotspots` (and pass it url of the 3D image as the only
parameter) and open the developer-console you can click around on your image and
the see the positions as console log outputs.

@Pannellum.hotspots(https://pannellum.org/images/bma-1.jpg)

## `@Pannellum.video`

                         --{{0}}--
Integrating a video happens similarly, but you will have to pass a unique
identifier and then the url of your video.

@Pannellum.video(vidID,https://pannellum.org/images/video/jfk.mp4)

## Implementation

                         --{{0}}--
Except of `@Pannellum.video`, all other panorama view macros are parametrized
calls of the macro `@Pannellum._panorama_`, which defines a target `div` and a
script to be executed. The delay is currently required, to deal with the loading
delay of the all CSS and JavaScript files. This will be fixed in the next
version of LiaScript.

````html
link:     https://pannellum.org/css/style.css
          https://cdn.pannellum.org/2.4/pannellum.css
          https://vjs.zencdn.net/7.1.0/video-js.css

script:   https://cdn.pannellum.org/2.4/pannellum.js
          https://vjs.zencdn.net/7.1.0/video.js
          https://pannellum.org/js/videojs-pannellum-plugin.js

@Pannellum.panorama: @Pannellum._panorama_(@uid,@0,{})
@Pannellum.panoramaWithHotspots: @Pannellum._panorama_(@uid,@0,```@1```)
@Pannellum.hotspots: @Pannellum._panorama_(@uid,@0, ,true)

@Pannellum._panorama_
<div id="panorama_@0" style="width: 100%; height: 400px;"></div>

<script>
  setTimeout(function(e) {
    let debug = "@3";
    pannellum.viewer('panorama_@0', {
          "type": "equirectangular",
          "hotSpotDebug": (debug == "true" ? true : false),
          "panorama": "@1",
          "autoLoad": true,
          "hotSpots": [@2]
    });
  }, 1000);
</script>
@end

@Pannellum.video
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
setTimeout(function(e) {
  videojs('@0', {
      plugins: {
          pannellum: {}
      }
  })}, 1000);
</script>

@end
````

                         --{{1}}--
If you want to minimize loading effort in your LiaScript project, you can also
copy this code and paste it into your main comment header, see the code in the
raw file of this document.

{{1}} https://raw.githubusercontent.com/liaTemplates/pannellum/master/README.md
