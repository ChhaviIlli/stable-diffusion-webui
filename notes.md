https://www.reddit.com/r/StableDiffusion/comments/xjvh05/gfpgan_and_codeformer_seperately_and_together/
GFPGAN and CodeFormer - seperately and together.
Comparison
I've seen discussion of GFPGAN and CodeFormer, with various people preferring one over the other. So I decided to test them both. I use the Colab versions of both the Hlky GUI (which has GFPGAN) and the Automatic1111 GUI (which has both GFPGAN and CodeFormer). The results were very interesting.

First, here's an image that I generated in Stable Diffusion (Scarlett Johansson as a space heroine):

https://i.imgur.com/PkW0T6r.png

As you can see, there are a lot of problems with the face, especially the eyes and mouth.

I ran it through GFPGAN in the Hlky GUI (at 100% strength; all of the examples I am posting here were done at 100% strength in GFPGAN, CodeFormer, or both), with this result:

https://i.imgur.com/GshgaUd.png

Curiously, running the image through GFPGAN in the Autmatic1111 version produced a different result, with slightly bigger eyes, a different eye color, and different lips. I'm not sure why this is. Here's the Automatic1111 GFPGAN result:

https://i.imgur.com/1uhFR9h.png

Both GFPGAN results are vastly better than the original image in terms of facial structure and eye appearance, but both also had the side effect (common with GFPGAN) of making the face look a little too smooth, textureless, and digital.

I then ran the original image through CodeFormer in the Automatic1111 GUI, and got this result:

https://i.imgur.com/198UrFF.png

It didn't fix the facial structure problems with the original image nearly as well as GFPGAN did, nor did it satisfactorily fix the eyes. However, it gives the face a more textured appearance that doesn't look as digital as the GFPGAN results.

This led me to suspect that combining GFPGAN and CodeFormer might produce better results than using either alone.

I ran the Hlky GFPGAN result through CodeFormer in the Automatic1111 GUI, and got this result:

https://i.imgur.com/hE3j48i.png

Also in the Automatic1111 GUI, I both tried running GFPGAN and CodeFormer simultaneously on the original image, and running CodeFormer alone on the previous Automatic1111 GFPGAN result. Both resulted in 100% identical images which looked like this:

https://i.imgur.com/i3XUI2O.png

The GFPGAN + CodeFormer results look better than either GFPGAN or CodeFormer alone, as they have the superior facial shape reconstruction and eye fixing of GFPGAN, but with texture added back with CodeFormer, helping to minimize the overly smooth "GFPGAN'ed look".

The one thing that I'm most curious about is why GFPGAN results look different coming from Hlky as opposed to Automatic1111 (both on 100% strength). I also can't decide which of the two looks better than the other.

EDIT: It turns out that I made a mistake. In the Automatic1111 GUI settings for fixing faces, I had turned both the "CodeFormer visibility" and "CodeFormer weight" settings all the way up to 1, thinking this was the maximum setting. Upon closer inspection, I discovered that while 1 is indeed the maximum setting for "CodeFormer visibility", for some reason, the "CodeFormer weight" setting is reversed, with 0 being maximum and 1 being minimum. This means that all of the pictures linked to above which have been run through CodeFormer have been run through it while it was on the maximum visibility setting, but the minimum weight setting. This obviously skews the results.

I corrected the settings so that CodeFormer would be at the maximum setting for both visibility and weight and ran more tests, the results of which are below.

The image corrected by CodeFormer (both visibility and weight at maximum):

https://i.imgur.com/20XKZhW.png

The image simultaneously corrected by both GFPGAN and CodeFormer:

https://i.imgur.com/XYjtnoh.png

The image first corrected in GFPGAN (in Automatic1111), then CodeFormer:

https://i.imgur.com/5g2WFw4.png

These new results have significantly changed my opinion of CodeFormer. It is far more powerful than I initially thought. It can add extremely realistic texture, to the point that if one sets it at maximum weight, the results look exactly like a photograph of real human skin. It's probably best to set the weight lower than maximum if one wants a more painterly look. It's the exact opposite of GFPGAN: instead of taking away skin detail and creating a digitally airbrushed look, it adds incredibly realistic skin detail. Not only that, but it can mostly fix problems with eyes and facial structure on its own, although I do think GFPGAN can do some things in that area better.

Its main weakness seems to be that it doesn't seem as good as GFPGAN at fixing the position that a person's eyes are pointing in/looking at (If you look carefully at the last two images, you can see that CodeFormer did not fix the right eye position as well as GFPGAN did, and running both GFPGAN and CodeFormer together also did not fix the eye position, running GFPGAN first then feeding the result through CodeFormer did fix the eye position).

Here is a link to the Imgur gallery of all of the images together (each labeled as what it is):

https://imgur.com/a/UIQ0heP
