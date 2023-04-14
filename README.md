![image](https://user-images.githubusercontent.com/76540311/231950396-ec719ae6-5718-4638-9130-b7295de7ff9d.png)

We're making cool scenes today. Screenshot-worthy. Maybe use Stable Diffusion and make it into an actual painting after you're done. :)

## Introduction to Terrains

Let's start off by making a new Terrain.

![image](https://user-images.githubusercontent.com/76540311/231859990-3f750903-d436-4527-8b69-af616a188aae.png)

It's gigantic. Yes! That's a good thing. Don't make it any smaller!

On the right are the Terrain tools.

![image](https://user-images.githubusercontent.com/76540311/231861632-427cb7af-5f6c-4cf8-a2b4-8908b21bf2ee.png)

You'll really only need to use the middle three: terrain, trees, and details. The names speak for themselves, but terrain
modifies the relative elevation and height map of our area, trees is meant for large structures, usually trees, but can 
also be houses, watchtowers, Minecraft villages, etc. while details are meant for the tiny things like shrubs and flowers.

The paintbrush lets us "paint" our terrain with elevation, however hilly, jagged, or valley-like you want.

![image](https://user-images.githubusercontent.com/76540311/231860343-7749e649-37e4-47c6-862c-3e56c46fd514.png)

If you're interested in the technology behind this, we're technically just using different shades of white on a height map, so the actual "terrain file" we're painting looks more like:

![image](https://user-images.githubusercontent.com/76540311/231861105-bc954c53-7cd3-49a0-ae66-7f2859947de1.png)

which you might've seen before from some elevation maps! The awesome thing about this is that we can take most any elevation map from online, import it into Unity, and already have a pre-made terrain. In fact, it's ridiculously easy to get real-life features, like Mount Fuji, in our game!

### Terrain Toolsets

Let's play around a little with the tools before we bring out the big guns.

In the first tab: "Terrain Tools", we see:

![image](https://user-images.githubusercontent.com/76540311/231860922-3bd64799-709e-4fae-8802-6d8e7465cea0.png)

and we can now click on our terrain and paint the Bob Ross mountain.

![image](https://user-images.githubusercontent.com/76540311/231862530-cc952546-b522-4563-80d2-83b86b41f29d.png)

However, we want a valley! Let's follow the instructions Unity provides and do "SHIFT-CLICK" to lower the terrain under our paint.

What's going on? ~ Only the part we edited seems to shrink. Why doesn't the floor lower?

![image](https://user-images.githubusercontent.com/76540311/231862809-fdb85403-dd01-4fbe-b8dd-b60427ca9b8d.png)

Well, think back to our "height map" technology behind our paint. Right now, pure black makes up the bottom, while our white brushes add height to the map. If we wanted depth, we would need our paint to be super-black! That can't happen, so our entire area needs to be gray, with darker regions denoting valleys, and lighter regions giving us hills.

Or, in simpler terms, we need to raise the whole terrain!

![image](https://user-images.githubusercontent.com/76540311/231864830-3c1948fa-e64d-44f8-8261-93ba974986f6.png)

![image](https://user-images.githubusercontent.com/76540311/231864894-58c8be69-885a-45e8-9e04-2b2f57c6c63a.png)

Go to Terrain Settings -> Height -> 9000! This actually isn't a lot in terms of our height map.
You can see other settings here, like heightmap resolution, which you can use to make your height map way more finely detailed,
so you could potentially make your player smaller enough to be on the terrain. Remember the scale of everything!


If you set height, you should notice your creations pop out! This is why you should adjust height at the start.. 
otherwise you might find some issues down the road when you need to create valleys (and might have to create entire new terrains!).

![image](https://user-images.githubusercontent.com/76540311/231864603-323d0023-81e8-46c0-b99c-f5340b622c0c.png)

Now, you're more than welcome to get right to make gorgeous mountains, valleys, and other cool things, but remember the limitations! There's **no such things as overhangs**, so no crazy Dr. Seuss mountains, or crazy cliff edges, etc! That's the limitation of height map technology.

![image](https://user-images.githubusercontent.com/76540311/231869505-79165d67-7b10-44ea-9891-cc3aadf573e6.png)

However, it serves as an important baseplate, which then we can use actual objects and mountain objects to create those overhangs and structures. 
Feel free to edit along, but more important, let's figure out how to use existing height maps!


## Importing Terrains

Now, let's import our own heightmap from the world wide web!

Go ahead and google "height map", "height map mountain", "height map river", etc!
We're looking for these black and white images.

![image](https://user-images.githubusercontent.com/76540311/231867076-f13f2162-d10c-421b-8ad6-e9c6b71b99a2.png)

Now, download one. There's one last thing we need to do before putting it in our game- it needs to be a .RAW file.
Don't worry, we can convert our format to .RAW.

If you want to save yourself the trouble of converting to .RAW before even seeing what your texture might look like, 
there are some handy browser tools that will visualize the simple PNG, JPG, TIFF, as a terrain in your browser! So, 
you don't have to spend time converting to get into Unity.

Here's one: https://imagetostl.com/create-3d-heightmap
And another: https://cpetry.github.io/NormalMap-Online/

If you're satisfied with what you see, or if you're feeling lucky, let's convert our photo to .RAW so Unity understands it.
The easiest way, as far as I'm concerned, is to just run these five lines of Python in the same directory as your image.
Make sure to "pip install Pillow".

```
from PIL import Image
import numpy

im = Image.open('input.tif') # Switch out 'input.tif' to your file's name!
imarray = numpy.array(im)
imarray.astype('int16').tofile("output.raw")
```

Finally, back in Terrain Settings, there's an option called "Import Raw..."

![image](https://user-images.githubusercontent.com/76540311/231868503-b7c5b253-4f81-445e-aae1-2f818d255962.png)

You can also "Export Raw..." if you're done something impressive with your existing heightmap.

Make sure to set the "Resolution" to the resolution of the image file you downloaded. Otherwise, some features may mess up!

![image](https://user-images.githubusercontent.com/76540311/231868704-21848cef-5d8c-4e04-b69c-560a122559f5.png)

Now, we can see our height map in Unity!

![image](https://user-images.githubusercontent.com/76540311/231866952-f39c1226-66c1-40ed-bd38-fd55ba17faa6.png)

(Here's a more impressive example.)

![image](https://user-images.githubusercontent.com/76540311/231868908-cf20e5de-6280-4aaa-8a3d-36bf9bfb6a5f.png)



## Texturing Terrains

At the top of Terrain Settings, we see a material slot.

![image](https://user-images.githubusercontent.com/76540311/231870858-a1c774db-a243-4413-b64e-fdf5f782d80c.png)

Change to SpatialMappingWireframe. This is just for fun!

![image](https://user-images.githubusercontent.com/76540311/231890056-8210dab5-0e43-4e53-a89a-e260e09cb6be.png)

Okay, now go back to Default-Terrain-Standard. Otherwise, our paint brushes are going to have a hard time.

Now, let's head back to the "Terrain Tools" -> Brushes!

This time, our brush is "Paint Texture".

![image](https://user-images.githubusercontent.com/76540311/231890258-6ed3f3bc-d1ba-4857-8092-2f2d48020bc6.png)

We will need a base layer! Choose the regions default color or pattern: rocks, sand, desert, grass..!

Let's head to your nearest search engine and grab a "seamless texture", or if you're hardcore, just the color you want as a picture.

Keywords like "low poly", "4k", "realistic", "game art" work especially well for finding certain textures.
If you were at my [AIGameDev workshop], you probably know and can generate your own seamless game texture too!

![image](https://user-images.githubusercontent.com/76540311/231891022-d76f71d0-a7b2-48a1-b2e9-cce108aba553.png)

Drag your image into your Unity Assets.
Now, we can "Create Layer". This will be our base layer, so choose the regions default color or pattern: rocks, sand, desert, grass..!

![image](https://user-images.githubusercontent.com/76540311/231890381-cd423cb8-8c3f-4d0f-9948-4ff25392cfaf.png)
![image](https://user-images.githubusercontent.com/76540311/231890355-8a9ef3f3-c347-4785-819c-da281fe98aa2.png)

Now, everything's colored! Use the dropdown to open your texture and adjust tiling as neccessary near the bottom of the right panel.

![image](https://user-images.githubusercontent.com/76540311/231891694-9c327431-a994-49ec-b81c-d18a1a5c1ca8.png)

We can rinse and repeat, by adding another layer, but this time, since we're not "at the bottom" anymore, you won't see this layer appear.
This layer instead will be on our brush, which we can click on the terrain to begin coloring in. Adjust opacity and size as need be!

![image](https://user-images.githubusercontent.com/76540311/231891563-a8b81c17-b7a5-452f-8469-34a95fa37171.png)

![image](https://user-images.githubusercontent.com/76540311/231891535-7acb8586-338c-4c74-ae0e-b1d45aa609a4.png)

Yes, you can also "import textures" like we did with our height map from the internet, but make sure the texture corresponds to your height map!
Afterwards, you would import it as your base layer, and adjust the tiling until it tiles as a once-over across your entire terrain.

![image](https://user-images.githubusercontent.com/76540311/231892097-cafec05d-af89-4c30-a662-f43ff40f0404.png)

If you really want to get into it, there are height maps and texture maps of anywhere in the world. You don't need to design the Kalahari~ import it! Here's an awesome resource for translating satellite images and height maps into your game's terrain: https://3d-mapper.com/heightmaps-and-textures/

Note that the precision of our satellites isn't all too great, so unless you come across a drone-scanned texture or height map, your results might be pretty far off from "playable drop-in world" without tuning or adjusting a lot.


## Trees 

Finally, let's spawn in trees. Well, "trees". They can be anything, really. Mostly trees, although.

In fact, let's do random things, just to prove a point.

Go to New -> 3D Object -> Randomly Click Anything.

Yes, anything! If you're feeling really brave, go import an fbx or obj file into Unity quickly. 
(https://sketchfab.com/search?q=free&type=models) This will be crazy.

![image](https://user-images.githubusercontent.com/76540311/231892656-d74a8dd8-3520-4559-927c-f5934d90ea14.png)

Alright, drag the object from your scene or your browser into "Assets" in order to make it a preset gameobject.

![image](https://user-images.githubusercontent.com/76540311/231892828-4867e0af-5764-4614-a2bb-bda581304df2.png)

Now, head over to "Paint Trees" on our Terrain:

![image](https://user-images.githubusercontent.com/76540311/231892885-1b1a986f-2687-458d-be80-9f1084bf2e2c.png)

![image](https://user-images.githubusercontent.com/76540311/231892949-c16f51f2-6bea-4971-a348-7a7e340be024.png)
![image](https://user-images.githubusercontent.com/76540311/231892975-ec8c2dea-e80d-48c8-b23f-82af723cf0d1.png)

"Edit Trees" -> "Add Tree"

Now, click the layer, and paint your scene as before! This time, we're spawning in millions of prefabs with our brush.

![image](https://user-images.githubusercontent.com/76540311/231893384-3877002c-359e-4bef-83ec-24a1b3c8684c.png)

The render distance is a little low. If you can handle it, go to "Terrain Settings", "Detail Objects", and max out all the render settings.

![image](https://user-images.githubusercontent.com/76540311/231893724-5c86cca6-b25d-42cd-9d37-45a86ba391a9.png)

Let's go wild. Back on the "Paint Trees" tab, click "Mass Place Trees".

![image](https://user-images.githubusercontent.com/76540311/231893910-067ed613-3df9-46b6-bfab-7b163fbeb6e8.png)

If you dared to choose anything other than a simple object for this task, watch out! Your computer will probably crash unless you
turn this number way down!

![image](https://user-images.githubusercontent.com/76540311/231894020-ecf6a8a4-4665-4eed-bdf7-7b99108ac144.png)

"Generate!!!"

![image](https://user-images.githubusercontent.com/76540311/231894100-55dcf86c-5698-4baf-89c4-bcaa98b07083.png)

A perfect vista.

Doing this with actual trees does work better, although. Here's a screenshot from a game I made awhile back using this exact technique:

![image](https://user-images.githubusercontent.com/76540311/231894332-aed2359b-66fc-4d03-8b8a-c79ded1c56d8.png)

Let's not go over "Paint Details" too much. It's the exact same thing, but details are more 2D cardboard cutouts, usually meant 
for grass, flowers, and other simple ground things.

Here's another screenshot from the same game, where I used "details" to texture all the grass. 

![image](https://user-images.githubusercontent.com/76540311/231894680-693c066e-f694-4f27-a1b2-4a2769758e75.png)


## General Environment

Let's finally look at skyboxes and other light sources.

On the top, go to "Window" -> "Rendering" -> "Lighting"

![image](https://user-images.githubusercontent.com/76540311/231895404-ece2413c-01c7-424f-b081-cd9bde18313a.png)

Now, on "Environment", set the values to anything and see the effect!

![image](https://user-images.githubusercontent.com/76540311/231895532-9f37ae55-706a-402a-97c5-4b46e08b88f5.png)

Fog really helps sell things. Here's my output:

![image](https://user-images.githubusercontent.com/76540311/231895630-33469301-f9fd-4b30-a063-9812ad067887.png)

If you want, you can import skyboxes and other assets and drop them in as easily as before.

Let me put a free tree from Sketchfab in..

![image](https://user-images.githubusercontent.com/76540311/231896088-3693cc7c-46be-4d3f-bcd8-142e0006033a.png)

This is bad on purpose, trust me..

Okay, now let's see the same tree after I stable diffusion it.

![image](https://user-images.githubusercontent.com/76540311/231925030-10a3bad1-a94a-4566-903d-48e51d65dec3.png)

![image](https://user-images.githubusercontent.com/76540311/231950445-863282ce-612c-46c4-a08a-25b9e7511b9d.png)

















