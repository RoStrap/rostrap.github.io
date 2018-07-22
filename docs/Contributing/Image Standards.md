# Image Standards

If uploading icons, images must be 2x size so that high-density screens can still appreciate the beautiful icons. Icons should also be white (so that you can change ImageColor3 to whatever you want, including black).

For example, for a 24x24 image (toggle_on) from [material.io](https://material.io/tools/icons/) we would download the following.

![](https://user-images.githubusercontent.com/15217173/41890727-644a7976-78d6-11e8-8294-8a1e8587d14f.png)

Go with the 48x48 image in the 2x folder.

![](https://user-images.githubusercontent.com/15217173/41890793-c204f226-78d6-11e8-86b6-444d9a6d9bdb.png)

Pixels of 100% transparency (0% opacity/alpha) must have white color values.

|Bad|Good|
|:-:|:--:|
|![](https://user-images.githubusercontent.com/15217173/41890220-21334f98-78d4-11e8-85c0-f053e12fe8df.png)|![](https://user-images.githubusercontent.com/15217173/41890355-c3b85790-78d4-11e8-99f0-e292f8669885.png)|

To fix this in GIMP, do the following. First, create a new layer:

![](https://user-images.githubusercontent.com/15217173/41890241-35d59adc-78d4-11e8-937d-0cd817cfdb2e.png)

Make sure it is filled with white pixels:

![](https://user-images.githubusercontent.com/15217173/41890244-3af198b8-78d4-11e8-9048-52e1b9d713f7.png)

Next, cut out all of the pixels, leaving only transparent white pixels. To do this, press `R` (open select tool), click on the image, hit `Ctrl + A` (select all), then hit `Ctrl + X` (cut). Click and drag on this transparent white layer and make sure it is on the bottom. Then `Right Click` + `Merge Down`

![](https://user-images.githubusercontent.com/15217173/41890502-63873c3c-78d5-11e8-8f0f-34b9074b20be.png)

Make sure to `save color values from transparent pixels` when you export the image.

![](https://user-images.githubusercontent.com/15217173/41890586-ba97e490-78d5-11e8-8f1f-0fe0e7fa2e87.png)
