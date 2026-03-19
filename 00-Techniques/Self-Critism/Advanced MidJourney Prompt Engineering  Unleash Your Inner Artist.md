---
title: Advanced MidJourney Prompt Engineering | Unleash Your Inner Artist
source: https://jamesbachini.com/advanced-midjourney-prompt-engineering/#midjourney-flags
author:
  - "[[JamesBachini.com]]"
published: 2023-01-20
created: 2025-09-08
description: As the leading AI image generator, MidJourney consistently produces stunning, high-quality images that range from the bizarre to the breathtaking. As someone who lacks artistic talent, I've taken the time to study and master this tool, and in this post I share my insights and tips for getting the mo
tags:
  - clippings
feature: thumbnails/external/d8f5975092fdb5652e1961ccdea315e3.png
thumbnail: thumbnails/resized/509421ebe370684a6c258c58f609a152_86cf658e.webp
---
[Skip to content](https://jamesbachini.com/advanced-midjourney-prompt-engineering/#wp--skip-link--target)

As the leading AI image generator, MidJourney consistently produces stunning, high-quality images that range from the bizarre to the breathtaking. As someone who lacks ~~artistic~~ talent, I’ve taken the time to study and master this tool, and in this post I share my insights and tips for getting the most out of it. Follow my *journey* as I delve into the world of AI-generated art and discover new ways to elevate my own creativity.

1. [MidJourney Commands](https://jamesbachini.com/advanced-midjourney-prompt-engineering/#midjourney-commands)
2. [Tips & Tricks](https://jamesbachini.com/advanced-midjourney-prompt-engineering/#tips-tricks)
3. [MidJourney Flags](https://jamesbachini.com/advanced-midjourney-prompt-engineering/#midjourney-flags)
4. [MidJourney Styles](https://jamesbachini.com/advanced-midjourney-prompt-engineering/#midjourney-styles)
5. [MidJourney Artists](https://jamesbachini.com/advanced-midjourney-prompt-engineering/#midjourney-artists)
6. [Example Prompts](https://jamesbachini.com/advanced-midjourney-prompt-engineering/#example-prompts)
7. [Combining An Image Editor](https://jamesbachini.com/advanced-midjourney-prompt-engineering/#Combining-An-Image-Editor)

---

## MidJourney Commands

To get started with MidJourney you need a Discord account and an invite link to the channel: [https://discord.gg/midjourney](https://discord.gg/midjourney)

You’ll get 25 credits for free which you can use in the Newbies channels or you can pay £12/month to get access via DM’s and additional credits. If you are interested in an open source alternative there is [Stable Diffusion](https://github.com/Stability-AI/stablediffusion).

Here are the basic commands:

**/imagine *prompt***

The prompt is where you will describe your image and add flags etc. I recommend crafting prompts in this formula

```
describe the image, describe the background, styles, --flags
```

Note that you can also put an image URL in the prompt if you want to create a variation on an existing image.

**/info**

Shows you your account balance details like that

**/settings**

Lets you adjust your settings, this is what I use currently:

![Midjourney settings](https://jamesbachini.com/wp-content/uploads/2023/01/image-2.png)

Midjourney settings

Remix mode is also worth trying as it let’s you edit your prompt as you create variations.

---

## Tips & Tricks

When crafting your prompt, it’s best to avoid using negative words like “not” or “without.” Instead, try using a phrase like “–no” followed by the thing you want to exclude. For example, “new girlfriend –no ai bot”

With ChatGPT the more info you give it the better, with MidJourney it’s different and too much detail can be overwhelming for the system, so try to stick to 2-3 core concepts in your prompt. Being concise and clear will help the AI generate more coherent images.

You can influence the importance of different elements in your prompt by assigning weights to them. For example, “new girlfriend::2 ai bot::-1” tells the AI to prioritize the concept of a “new girlfriend” over “ai bot.”

If you end up with a.webp image, don’t panic! Just wait a little longer for it to fully render, and then reopen the image to get a.png version.

For a cohesive brand, it’s a good idea to choose a specific style and then append it to the end of every prompt you generate for that brand. This will help ensure that all of your generated images have a consistent look and feel.

To combine multiple prompts, use brackets. For example, “\[new girlfriend\] + \[beautiful beach\] –ar 2:3” tells the AI to generate an image featuring a “new girlfriend” and a “beautiful beach”

![What's the mother like?](https://jamesbachini.com/wp-content/uploads/2023/01/image-4-200x300.png)

What's the mother like?

---

## MidJourney Flags

There’s a full list of options you can set as flags [here](https://midjourney.gitbook.io/docs/imagine-parameters) but these are the most important ones you need to know

```
--v 4 = use a specific version of Midjourney
--ar 3:2 = 3:2 aspect ratio
--stylize = defines how much "beauty" MidJourney should add to make the image aesthetically pleasing
--q 2 = twice the quality twice the cost/time
--video = then send a email emoji and it will send you a video of the creation process
--uplight = upscale without adding additional detail
```

---

## MidJourney Styles

There are endless styles but this is a list I’ve compiled which I find useful for the what I want it to do. You can simply add as many of these as you want on separated by commas.

```
painting, drawing, sketch, oil on canvas, graffiti, watercolor painting, ink, pencil art, charcoal art, masterpiece, manga, hyperrealistic, cartoon, unreal engine, vector

vintage photo, black and white, sepia tone, pixar, cinematic lighting, volumetric lighting, vignete, minimalist, cyberpunk, 8k, octane render, 32-bit isometric, 16-bit adventure game, phantasmal iridescent, diagramatic drawing
```

---

## MidJourney Artists

You can add any popular artist but some work better than others. I went through the list on the MidJourney docs and added a few of my own which I feel gives a broad range of styles. The prompt used was the same for all of these:

```
An apple tree in a field in the style of an Akira Toriyama painting --ar 3:2
```
![](https://jamesbachini.com/wp-content/uploads/2023/01/AkiraToriyama-1024x683.png)

Akira Toriyama

---

## Example Prompts

```
/imagine a detailed mecahnical drawing of a robot in pencil on faded paper, artistic, vintage --ar 3:2 --q 2
```
![midjourney robot](https://jamesbachini.com/wp-content/uploads/2023/01/image-5-1024x683.png)

midjourney robot

```
/imagine an old woman standing in a field in front of a futuristic city of skyscrapers in the background, with a stormy sky, post apocolyptic, unreal engine, hyperrealistic, 8k, cinematic lighting --ar 3:2 --q 2
```
![midjourney woman](https://jamesbachini.com/wp-content/uploads/2023/01/image-7-1024x683.png)

midjourney woman

```
/imagine a glass globe of the world hanging in space with the sun shining through it and light reflecting off in to a background of stars and galaxies, detailed, 8k, artistic, lens flare --ar 3:2
```
![midjourney globe in space](https://jamesbachini.com/wp-content/uploads/2023/01/image-9-1024x683.png)

midjourney globe in space

```
/imagine a old fashioned horse and cart going down a cobbled victorian street in London in the year 1900, volumetric lighting, charcoal art, black and white --ar 3:2
```
![midjourney horse and cart](https://jamesbachini.com/wp-content/uploads/2023/01/image-6-1024x683.png)

midjourney horse and cart

```
/imagine a racing car melting in the desert surrounded by men on horses looking at the driver, in the style of salvador dali, mexico, cliffs, catus, sepia tone, vignette --ar 3:2
```
![midjourney painting](https://jamesbachini.com/wp-content/uploads/2023/01/image-10-1024x683.png)

midjourney painting

---

## Combining An Image Editor

MidJourney becomes even more powerful with some basic image editing knowledge. In this example I’ll get MidJourney to design a logo and then import that into an image editor such as inkscape, gimp, photoshop or canva to create a final design.

Let’s start with the prompt and then create variations followed by upscaling a favourite.

```
/imagine a logo for a blockchain project using hexagons, vector format, minimalist, modern, gradients
```
![](https://jamesbachini.com/wp-content/uploads/2023/01/image-8.png)

From here we can cut out the background and add some text to get a basic logo banner for our startup.

![](https://jamesbachini.com/wp-content/uploads/2023/01/ZKAI-1024x576.png)

---

There is a lot this tool can do and I plan to use mid journey for images on my blog, newsletter, in my videos. It wont be long before you can write prompts for video scripts with animations to fill scenes and do b-roll.

If you spend time editing images and creating content then it’s worth experimenting with this tool and other emerging AI tech to enhance your creativity and productivity.

---

Get [The Blockchain Sector Newsletter](https://bachini.substack.com/), binge the [YouTube](https://www.youtube.com/c/JamesBachini?sub_confirmation=1) channel and connect with me on [Twitter](https://twitter.com/intent/follow?screen_name=james_bachini)

- [YouTube](https://www.youtube.com/c/JamesBachini?sub_confirmation=1)
- [Twitter](https://twitter.com/intent/follow?screen_name=james_bachini)
- [LinkedIn](https://www.linkedin.com/in/james-bachini/)
- [Instagram](https://www.instagram.com/jamesbachini/)
- [TikTok](https://www.tiktok.com/@jamesbachini)
- [GitHub](https://github.com/jamesbachini)

*The Blockchain Sector* newsletter goes out a few times a month when there is breaking news or interesting developments to discuss. All the content I produce is free, if you’d like to help please share this content on social media.

Thank you.

![James Bachini](https://jamesbachini.com/wp-content/uploads/2022/11/signature_grey.png)

James Bachini

**Disclaimer**: Not a financial advisor, not financial advice. The content I create is to document my journey and for educational and entertainment purposes only. It is not under any circumstances investment advice. I am not an investment or trading professional and am learning myself while still making plenty of mistakes along the way. Any code published is experimental and not production ready to be used for financial transactions. Do your own research and do not play with funds you do not want to lose.