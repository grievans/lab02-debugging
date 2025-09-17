# My Submission

Griffin Evans
  Didn't really directly work with another team member per se but I should note I did talk some with others (e.g. Avi, Ruben) at the same table cluster and was influenced in what I looked for some by what other people were talking about.

[Shadertoy link](https://www.shadertoy.com/view/tclBDf)

Bugs found:

1. Changing `vec uv2` to `vec2 uv2`: found through simply seeing the editor highlight the syntax error.
2. Changing `raycast(uv, dir, eye, ref);` to `raycast(uv2, dir, eye, ref);`: noticed that the value of uv2 went unused and that this corresponded to how the view seemed to be zoomed in to just be one of the corners (with `uv` being [0,1] rather than `uv2`'s [-1,1] in both the x and y).
3. Changing `H *= len * iResolution.x / iResolution.x;` to `H *= len * iResolution.x / iResolution.y;`: noticed that x / x will always be 1 (assuming x nonzero) and thus that this line must not be made properly, and given that this seems to be meant to calculate the ratio of the image dimensions (x relative to y since this is the "H" horizontal vector) it made sense to change the latter to y.
4. Changing `dir = reflect(eye, nor);` to `dir = reflect(dir, nor);`: could see that the reflections were not being drawn properly, so searched the word "reflect" to find the parts where reflection was happening. Then looking at through the lines to try to follow what was happening logically, knew that the direction of the reflected march should correspond to the reflection of the direction of the ray hitting this intersection about the normal at that intersection. In the subsequent call to `march()` this `dir` is being passed in as the direction, so looked at this line to see if that matched the input variables I expected, which it didn't (since `eye` is the position of the eye and we want instead to use the direction from the eye to that point, i.e. `dir`).
5. Changed the thresholds for i and m in march: `i < 64` to `i < 256` and `m < 0.01` to `m < 0.005`. I'm not sure if one would necessarily consider this a bug as it's more subjective as to what are acceptable for maximum view distances and amount of distortion about rays nearly parallel to surfaces (given we're using spheremarching one should expect we have some degree of it so it's a matter of minimizing it while remaining performant), but I noticed the example output had both a longer draw distance for the checkered floor and significantly less noticeable gaps about the sides of the spheres, and so changed these values until they produced an image which appears the same to me.


# lab02-debugging

# Setup 

Create a [Shadertoy account](https://www.shadertoy.com/). Either fork this shadertoy, or create a new shadertoy and copy the code from the [Debugging Puzzle](https://www.shadertoy.com/view/flGfRc).

Let's practice debugging! We have a broken shader. It should produce output that looks like this:
[Unbelievably beautiful shader](https://user-images.githubusercontent.com/1758825/200729570-8e10a37a-345d-4aff-8eff-6baf54a32a40.webm)

It don't do that. Correct THREE of the FIVE bugs that are messing up the output. You are STRONGLY ENCOURAGED to work with a partner and pair program to force you to talk about your debugging thought process out loud.

Extra credit if you can find all FIVE bugs.

# Submission
- Create a pull request to this repository
- In the README, include the names of both your team members
- In the README, create a link to your shader toy solution with the bugs corrected
- In the README, describe each bug you found and include a sentence about HOW you found it.
- Make sure all ~~three~~$$\color{red}one$$ of your shadertoy~~s~~ are set to UNLISTED or PUBLIC (so we can see them!)
