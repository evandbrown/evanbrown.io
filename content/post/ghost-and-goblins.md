+++
comments = true
date = "2015-02-04T12:31:22-07:00"
draft = false
image = "img/symlink_1-1423668786097.png"
menu = ""
share = true
slug = "ghosts-and-goblins"
tags = ["tech"]
title = "Ghosts and Goblins: Customizing a Ghost Blog Theme"

+++

I wanted to write, and a requirement was a pretty site I could get running quickly. I chose Ghost (hosted at [ghost.org](http://ghost.org)) and purchased the [Goblin theme](http://themeforest.net/item/goblin-minimalist-contentfocused-theme/8576493). I'm happy with the result - I think it's pretty - and I'm going to talk about how I tweaked the theme and got going in less than a day.

## Ghost Theme Marketplace

The [Envato Market](http://themeforest.net/category/blogging/ghost-themes) for Ghost themes is solid. There are lots of beautiful themes and they all have live demo sites. It was easy to narrow the choice down to a few and settle on Goblin quickly. I PayPal'd $19, got a link to download the theme, and unzipped the download. Here's what I got:

![](/img/unzip-1423668770154.png)

Do open `document/index.html` and go through it. You'll learn that there are [4 versions of the theme](http://themeforest.net/item/goblin-minimalist-contentfocused-theme/full_screen_preview/8576493), and get prescriptive guidance for most of the setup. 

## Navigating the sample styles
I wanted to try out the 4 versions of the theme locally, so I installed Ghost to `~/dev/Ghost`. I unpacked Goblin to `~/dev/ghost-themes/goblin` and initialized a git repo to track my changes:
{{< highlight sh "style=friendly" >}}
git init
git add .
git commit -m "Initial commit"
{{< /highlight >}}

The default theme is in `goblin/default`, the 4 derivative versions are in `goblin/redefined/style[1-4]`. The `package.json` for each theme has the same name (Goblin) and version (1.1.2). To differentiate them after installing, I edited each one and added its style number. For example, for `style2` I edited `~/dev/ghost-themes/goblin/theme/redefined/style2/goblin/package.json`:
{{< highlight json "style=friendly" >}}
{
"name": "Goblin",
"version": "1.1.2-style2",
"description": "A minimalist and content-focused theme for Ghost",
"url": "http://previews.sunflowertheme.com/ghost/goblin",
"author": {
  "name": "sunflowertheme",
  "email": "support@sunflowertheme.com",
  "url": "http://www.sunflowertheme.com"
}
{{< /highlight >}}

Then I symlinked each of the styles into the local Ghost install:

![](/img/symlink_1-1423668786097.png)

Start Ghost and they're all there to play with:

![](/img/themes-1423668794456.png)

## Create Résumé, About, and Contact Pages
The resume, about, and contact pages on this theme stood out to me in the live demo and it's one of the main reasons I purchased it. I was surprised to see there was zero documentation on how to set them up! If you click one of the menu items, you'll get a 404 (a beautifully designed 404.)

I figured out the roundabout way that you need to create posts with URLs `resume`, `about`, and `contact`, and check `Turn this post into a static page` for each of them. But here's the real lesson: **read the 'Import Demo Content' section in the theme's documentation**. It will import a number of sample pages - including the ones described here - that are very useful to have locally as a reference. Lots of good design you can mimic.


## Disabling Superfluous Stuff
I found a few things I didn't like about the Goblin theme. Here's how I disabled them.

### 'Try Me' Hover Text
Background images in this theme are dope. Click the camera icon and you can see the original. But the big hovering 'Try me!' text is no bueno. 

![](/img/tryme-1423668802575.png)

Get rid of it by editing `goblin/assets/js/main.js` and doing a find and replace on `title="Try me!"`. You could also probably knock this out with a jQuery one-liner, but I wanted it gone forever.

### Scrolling 'Time to Complete'
Scrolling through a post shows a totally inaccurate and visually distracting "n minutes left" that follows the scrollbar.

![](/img/time-1423668809973.png)

Nope nope nope. Knock out lines 1125-1131 of the same `main.js` we mentioned earlier:

{{< highlight javascript "style=friendly" >}}
if($('body').is('.post-template') && !$('body').is('.page') && $('.post-content').length){
  sfApp.timeToRead();
}
{{< /highlight >}}

You could probably track down a CSS class and hide the timer, but I wanted to erase it.

### After-Post Share and Author Info
I dithered on these two a bit, but ultimately decided I wanted Disqus comments to follow a post and nothing else:

![](/img/postpost-1423668817125.png)

Create a new file `goblin/assets/css/custom.css` and fill it with this:

{{< highlight css "style=friendly" >}}
.share-box, .post-footer {
  display: none;
  visibility: hidden;
}
{{< /highlight >}}

Then modify `goblin/default.hbs` to include this new stylesheet after `css/colors/default.css` (~line 49):

{{< highlight javascript "style=friendly" >}}
<link rel="stylesheet" type="text/css" href="{{asset "css/custom.css"}}" />
{{< /highlight >}}

Boom! All gone.

## Conclusion
I really like the Goblin theme. The documentation was solid, and it took less than an hour (having never touched Ghost before) to make these changes. 

