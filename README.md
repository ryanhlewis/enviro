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








