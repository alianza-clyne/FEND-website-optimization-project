# Website Optimization Project

For this project, I will be optimizing a website.
The optimized site can be found here: https://alianza-clyne.github.io/website-optimization-project/


## Step One: Optimize The Site's Images
----------------------------------------------
Believe it or not, as small as they are, the images on this site are currently taking up a significant portion of the site's space. This not only results in the site's optimization being reduced, but it can also result in the images taking a while to load.

1. Using [Optimizilla](http://optimizilla.com/), I compressed all of the images on the site. This allowed me to save several bytes of date and improve the site's load time.

## Step Three: Let's Get Rid Of That Render Blocking Web Font
----------------------------------------------
Oh yes, you read that right. Linking Web fonts such as Google fonts in the head of your HTML file can actually result render blocking. This means that until the fonts has been loaded, the rest of site rendering is blocked. Nevertheless, there is a way around this!

Through using the [Web Font Loader](http://bit.ly/2DZjhJR), I was able to remove the Open Sans Google Font from the head of index.html, and put it in a Script tag. This gives me the power to ensure that the font loads asynchronously so that it does not render block.

See it for your self. Here's what the Google web font initially looked like when it was in the head of index.html.

```html
<link href="//fonts.googleapis.com/css?family=Open+Sans:400,700" rel="stylesheet">
```

To use the Web Font Loader instead, either remove the code above or comment it out, and then add the following script tags at the end of the index.html file.

```javascript
<script async src="https://ajax.googleapis.com/ajax/libs/webfont/1.6.26/webfont.js"></script>
<script>
WebFont.load({
google: {
  families: ['Opem Sans', 'sans-serif']
  }
});
</script>
```

## Step Three: 
----------------------------------------------
