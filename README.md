# Low Light Phone Photography

## Unlock your phone camera's full low-light potential:
Use an app like ProShot that allows you to 
crank ISO high 
and set shutterspeed slow, 
and disable build-in denoising, 
and enable raw capture if possible.

### Lock-off
- No movement, Tripod-like
- Use a phone stand, or lean phone against an object
- Set shutterspeed as slow as your phone allows (check if overexposed and reduce ISO if so) and Use ProShot's light painting feature (averages many shots).
### Handheld
- Be as stable as you can, find something to lean (your wrists/elbows/shoulders) against like a bicycle saddle, or sit on the ground.
- Set shutterspeed as slow as you can while preventing motion blur: Standing: 1/20 - 1/8, sitting/leaning: 1/8 - 1/2
#### segmented long exposure
- Take a burst, via ProShot's burst mode, or hold the shutter.
- **Align** the handheld frames via hugin or [Photopea](https://www.photopea.com/)
  (edit > auto-align, or manually align. btw photopea has scripting)
Already aligned images can be averaged with magick in termux ``magick "*.jpg" -evaluate-sequence mean "average.jpg"``
if aligning is too slow, do the next step (Binning) first: 

## Reduce Noise
- **Binning**: improve signal to noise ratio by averaging blocks of pixels into one (but reduces resolution).
Can be done via image magick in Termux: ```for file in *.jpg; do magick "$file" -resize 50% "${file%.jpg}_half.jpg"; done``` 
or via [imageJ](ij.imjoy.io/) (Image > Transform > Bin)
- **AI Denoising**
https://ai.nero.com/denoiser
(Make a new account if you run out of credits. Tip: use protonmail as email (doesn't require phone number to create and bypasses temp-mail detection).)
*Prebinning* gives better results in my experience (halfres or quarterres as input).

My method for final image: 
(Photopea.com)
- align
- average
- recover moved areas (like people) by masking them back in from frames where they didn't move.
- (magick) bin average to halfres and quarterres.
- (ai.nero.com) denoise fullres (or halfres) and quarterres with nero ai denoiser.
- mix the binned halfres with the denoised fullres and denoised quarterres.
