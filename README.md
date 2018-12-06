# Website Optimization Project

Udacity has challenged me to optimize Cameron's portfolio website, and fix a few performance related issues on his pizzeria site. It was a long journey, but like the adventurous coder I am, I conquered it! See the following for the steps that I took to make the magic happen.

# Section One: Optimize index.html
In this section, I will be working to optimize index.html so that it reaches a [PageSpeed](https://developers.google.com/speed/pagespeed/insights/) score of 90%.

You can view the original repository before my optimizations were applied to it on Udacity's Github [HERE](https://github.com/udacity/frontend-nanodegree-mobile-portfolio). Simply fork or download the repository and open up index.html.

As an alternative, you can view the edited repository that contains all of the optimizations on Alianza's Github [HERE](https://github.com/alianza-clyne/website-optimization-project). Simply fork or download the repository and open up index.html.

## Step One: Optimize The Site's Images
----------------------------------------------
Believe it or not, as small as they are, the images on this site are currently taking up a significant portion of the site's space. This not only results in the site's optimization being reduced, but it can also result in the images taking a while to load.

1. Using [Optimizilla](http://optimizilla.com/), I compressed all of the images on the site. This allowed me to save several bytes of date and improve the site's load time.

## Step Two: Let Go Of That Render Blocking Web Font
----------------------------------------------
Oh yes, you read that right. Linking web fonts such as Google fonts in the head of your HTML file can actually result in render blocking. This means that until the fonts have been loaded, the rest of site rendering is blocked. Nevertheless, there is a way around this!

Through using the [Web Font Loader](http://bit.ly/2DZjhJR), I was able to remove the Open Sans Google Font from the head of index.html, and put it in a Script tag. This gives me the power to ensure that the font loads asynchronously so that it does not render block.

See it for your self. Here's what the Google web font initially looked like when it was in the head of index.html.

```html
<link href="//fonts.googleapis.com/css?family=Open+Sans:400,700" rel="stylesheet">
```

To use the Web Font Loader instead, either remove the code above or comment it out and then add the following script tags towards the end of the index.html file.

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
I have also changed the media type in the print.css stylesheet link in the index.html file so that it reflects this.

```HTML
<!-- Original stylesheet code -->
<link href="css/print.css" rel="stylesheet">

<!-- New code -->
<link href="css/print.css" rel="stylesheet" media="print">
```
## Step Four: To or To Not Inline
----------------------------------------------
Now that css/print.css is no longer render blocking on all media types, we must take a look at css/style.css. This stylesheet contains styles that are meant to be used for all media types when they access index.html. Since the file only has 49 lines of code, I have decided to inline the css/style.css code in the index.html file. I will then comment out the link to the css/style.css file. This will allow the website to render faster.

Here's what this would look like in the index.html file.

```HTML
<!-- Before CSS inline -->
<link href="css/style.css" rel="stylesheet">

```

```css
/* After CSS inline */
<style>
/* For optimization purposes, I have inlined the code in the css/style.css file.*/
html {
  font-size: 100%;
  overflow-y: scroll;
  -webkit-tap-highlight-color: rgba(0,0,0,0);
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: none;
}
body { margin: 0; font-size: 14px; line-height: 1.61; font-weight: 400; }
body, button, input, select, textarea { font-family: 'Open Sans', sans-serif; color: #333; }

a { color: #12C; }
a:visited { color: #61C; }
a:focus { outline: thin dotted; }
a:hover, a:active { color: #c00; outline: 0; }

b, strong { font-weight: bold; }
pre, code { font-family: monospace, monospace; font-size: 1em; }
ul, ol { margin: 1em 0; padding: 0 0 0 20px; }
img { border: 0; max-width: 100%; }

body { background: #fff; }
header, footer, .container { max-width: 45em; margin: 0 auto; }

header { padding: 0 0.5em; color: #C90B0B; }
header img { border-radius: 40px; float: left; }
header p { font-size:1.5em; font-weight: bold; padding-left: 4em;}
header p span { font-size: 0.8em; font-weight: normal;}

.hero { padding: 2em; background-color: #f8f8f8; font-size:1.2em;
  border-bottom: 1px solid #ccc;
  border-top: 1px solid #ccc;
}

.content { padding: 1em 1em; }
.content li { list-style-type: none; font-size: 1.1em;}
li img { float:left; padding-right: 1em; }
li p { font-size: 0.9em; font-style: italic; }

footer {
  padding: 0 0.5em;
  border-top: 1px solid #ccc;
}
footer span { float: right; font-style: italic; }

/* Smartphones (portrait) */
@media only screen and (max-width: 480px) {
  body { font-size: 12px;}
  header p { padding-left: 4.5em;}
}
</style> 
```

## Step Five: It's Time For JavaScript to Move Out
----------------------------------------------
Currently, most of the JavaScript files are linked in the head of index.html. Since JavaScript controls the function of the site (instead of the visual representation as HTML and CSS do) and is render blocking, I have moved script tags for Google Analytics and js/perfmatters-min.js to the bottom of the body section.

Here's what this would look like.

```JavaScript
/*  Before script tags are moved */
<head>
<script>
  (function(w,g){w['GoogleAnalyticsObject']=g;
  w[g]=w[g]||function(){(w[g].q=w[g].q||[]).push(arguments)};w[g].l=1*new Date();})(window,'ga');

  // Optional TODO: replace with your Google Analytics profile ID.
  ga('create', 'UA-XXXX-Y');
  ga('send', 'pageview');
</script>
<script src="http://www.google-analytics.com/analytics.js"></script>
<script async src="js/perfmatters-min.js"></script>
</head>

/*After script tags are moved*/
<body>
<script>
  (function(w,g){w['GoogleAnalyticsObject']=g;
  w[g]=w[g]||function(){(w[g].q=w[g].q||[]).push(arguments)};w[g].l=1*new Date();})(window,'ga');

  // Optional TODO: replace with your Google Analytics profile ID.
  ga('create', 'UA-XXXX-Y');
  ga('send', 'pageview');
</script>
<script src="http://www.google-analytics.com/analytics.js"></script>
<script async src="js/perfmatters-min.js"></script>
</body>
```

### Step Six: It's Minification Time
----------------------------------------------
Spaces in HTML, CSS, and JavaScript files can take up quite a bit of space and thus result in the site's optimization being reduced.

As a result, I minified index.html using the [HTML Minifier](http://kangax.github.io/html-minifier/). For the sake of preserving the readability of the HTML file, I changed the name of the original index.html file to index-unminified.html. I then created another file for the minified HTML and named it index.html.

I also minified js/perfmatters.js using the [JavaScript Minifier](https://javascript-minifier.com/) and changed the file name to perfmatters-min.js to reflect this update.

### Step Seven: The Final Product
----------------------------------------------
Here's what the page speed of the index.html file looked like before these optimizations.
![Image of mobile pagespeed before optimizations](https://image.ibb.co/jjxQKn/before_mobile.jpg)
![Image of website pagespeed before optimizations](https://image.ibb.co/dqnQKn/before_website.jpg)

Here's what the pagespeed of the index.html file looked like after these optimizations.
![Image of mobile pagespeed after optimizations](https://image.ibb.co/eLzSX7/after_mobile.jpg)
![Image of website pagespeed after optimizations](https://image.ibb.co/noNEC7/after_website.jpg)

You can try it out for yourself by heading on over [Google Page Speed Insights](https://developers.google.com/speed/pagespeed/insights/) and entering https://alianza-clyne.github.io/FEND-website-optimization-project/ into the search box.

### Future Improvements: Leverage [Browser Caching](https://varvy.com/pagespeed/cache-control.html)
----------------------------------------------
In the future, I'd like to try utilizing browser caching in order to further optimize index.html.

# Section Two: Removing the Jank From pizza.html
For this section, I will be making optimizations to views/js/main.js which is linked to views/pizza.html. My goal is to ensure that views/pizza.html renders with a consistent frame-rate of 60 frames per second when I scroll through the site.

Furthermore, I'd also like to ensure that the time needed to resize the pizzas in views/pizza.html is less than 5 ms. I will make this magic happen by making changes to the pizza size slider on the views/pizza.html page. The resize time will be shown in the Chrome browser's developer tools.

You can view the original repository before my optimizations were applied to it on Udacity's Github [HERE](https://github.com/udacity/frontend-nanodegree-mobile-portfolio). Simply fork or download the repository and click on the "views" folder. Then open up pizza.html.

As an alternative, you can view the edited repository that contains all of the optimizations on Alianza's Github [HERE](https://github.com/alianza-clyne/website-optimization-project). Simply fork or download the repository and click on the "views" folder. Then open up pizza.html.

## Step One: Improve Frame Rate
----------------------------------------------
1. In order to improve the frame rate of views/pizza.html so that it renders at 60 frames per second (or approximately 16 milliseconds), I compressed the pizza.png image that appears in the background of the views/pizza.html site.

2. I also replaced the document.querySelector with
document.getElementById in the function changeSliderLabel(size) because using getElementById will
 result in the element being fetched faster. This optimizes the website.

3. I changed querySelector() to getElementById(). The reason for this is because using getElementById will result in the element being fetched faster and thus, the page will be more optimized. I applied this change to the function updatePositions().

4. I have also chosen to reduce the amount of times that the
  for loop in addEventListener() will be called/looped from 200 to 21. This will help to optimize the site when scrolling.

Note: All optimizations have the word "Optimization" listed above them in the views/js/main.js document.


## Step Two: Computational Efficiency--Resizing The Pizzas  
----------------------------------------------
1. In order to ensure the time needed to resize the pizzas (this is done by dragging the horizontal pizza mover) is less than 5 ms, I  replaced the document.querySelector with document.getElementById in the functions changeSliderLabel(size), determineDx (elem, size) because using getElementById will result in the element being fetched faster. 

2. I also removed document.querySelectorAll(".randomPizzaContainer") from the changePizzaSizes(size) function. The reason for this is because document.querySelectorAll(".randomPizzaContainer") is called multiple times in the function. Instead of having to constantly repeat this step, I felt it would be better to set document.querySelectorAll(".randomPizzaContainer") to be equal to the variable pizzaContainerItems so that going forward, I can simply call pizzaContainerItems which will assist with optimizing the pizza
size slider. 

On top of this, I replaced the document.querySelector with document.getElementsByClassName because using getElementsByClassName will
result in the element being fetched faster.

3.  I removed the following lines of code from the for loop in changePizzaSizes:

    var dx = determineDx(document.querySelectorAll(".randomPizzaContainer")[i], size);

     AND

    var newwidth = (document.querySelectorAll(".randomPizzaContainer")[i].offsetWidth + dx) + 'px';

My reason for doing this is that here we are simply setting code to be equal to variables. Essentially, this is something that will always remain constant within the changePizzaSizes function and thus, there's no real benefit in keeping it in the for loop.
Furthermore, keeping it in the for loop actually reduced the slider's optimization as it was constantly being forced to repeat these two unnecessary steps.

I also replaced (document.querySelectorAll(".randomPizzaContainer") with the variable pizzaContainerItems. I did this because I have already set pizzaContainerItems to be equal to document.getElementsByClassName("randomPizzaContainer") which would almost be the equivalent to (document.querySelectorAll(".randomPizzaContainer").

4. I changed the for loop in changePizzaSizes from
    for (var i = 0; i < document.querySelectorAll(".randomPizzaContainer").length; i++)
    
    to
    
    for (var i = 0, pLength = pizzaContainerItems.length; i < pLength; i++).

Essentially, I replaced document.querySelectorAll(".randomPizzaContainer").length with pizzaContainerItems.length. To make this easier to call later, I have set pizzaContainerItems.length to equal the variable pLength.

Then I set it so that the variable i is less than pLength like the original for loop.

Note: All optimizations have the word "Optimization" listed above them in the views/js/main.js document.

## The Final Product
----------------------------------------------
According to the console, the frame rate while scrolling is 60 frames per second (approximately 16 ms) or less and the amount of time to resize the pizzas is less than 5 seconds.
![Image showing 60 frames per second in console](https://image.ibb.co/d8AnCS/after_fps_scripting_time_1.jpg)
![Image showing resize time in console](https://image.ibb.co/ie0nCS/after_fps_scripting_time_2.jpg)
