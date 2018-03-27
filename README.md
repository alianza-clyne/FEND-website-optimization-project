# Website Optimization Project

For this project, I will be optimizing a website.
The optimized site can be found here: https://alianza-clyne.github.io/website-optimization-project/

# Section One: Optimize index.html

## Step One: Optimize The Site's Images
----------------------------------------------
Believe it or not, as small as they are, the images on this site are currently taking up a significant portion of the site's space. This not only results in the site's optimization being reduced, but it can also result in the images taking a while to load.

1. Using [Optimizilla](http://optimizilla.com/), I compressed all of the images on the site. This allowed me to save several bytes of date and improve the site's load time.

## Step Two: Let Go Of That Render Blocking Web Font
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

## Step Three: Add a Media Query That Limits When print.css Is Called
----------------------------------------------
The file under css/print.css specifies styles that will be used on the website when the viewer requests to print the page. The reality is that most users probably won't be going to Cameron's portfolio site to print it. Now, we could leave print.css in one peace, but unfortunately for that file, it is blocking the rendering of Cameron's portfolio site which makes it slower for us! So you know what this means? It's canning time!

![Just kidding GIF](https://media.giphy.com/media/l0MYR62XwdexZfLt6/giphy.gif)

Okay, just kidding! We will actually be using a media query that only allows the browser to render print.css if the media is set to "print". Essentially, this means that print.css will only be used if the site user requests to print the webpage. Here's what this would look like in the print.css code.

```css
/* Original print.css code */
@media print {
  * { background: transparent !important; color: black !important; text-shadow: none !important; filter:none !important; -ms-filter: none !important; }
  a, a:visited { color: #444 !important; text-decoration: underline; }
  a[href]:after { content: " (" attr(href) ")"; }
  tr, img { page-break-inside: avoid; }
  img { max-width: 100% !important; }
  @page { margin: 0.5cm; }
  p, h2, h3 { orphans: 3; widows: 3; }
  h2, h3{ page-break-after: avoid; }
}

/* print.css code after media query is applied to it */
@media only print {
  * { background: transparent !important; color: black !important; text-shadow: none !important; filter:none !important; -ms-filter: none !important; }
  a, a:visited { color: #444 !important; text-decoration: underline; }
  a[href]:after { content: " (" attr(href) ")"; }
  tr, img { page-break-inside: avoid; }
  img { max-width: 100% !important; }
  @page { margin: 0.5cm; }
  p, h2, h3 { orphans: 3; widows: 3; }
  h2, h3{ page-break-after: avoid; }
}
```
