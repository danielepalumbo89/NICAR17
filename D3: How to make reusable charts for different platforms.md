# D3.js: How to make reusable charts for different platforms
## Daniele Palumbo, International Business Times UK       |      Twitter: @danict89


# Key points:

Background: https://bost.ocks.org/mike/chart/

## 1 - Configuration
  When learning d3.js, the way we learn how to structure the code is crucial. Setting now the code with in mind                 reusability will help us to not change the code everytime we need a new chart or we have a new dataset. 

      function chart() {
      // your chart here
      }
      
  Creating the chart as function will save us time because we will be able to include the main part of the chart (data, axis,   scales, labels) all in one place, styling them in a separate file.
      
## 2 - Re-configuration
   This is the tricky part. 
   Github is the best source of libraries we can use to create a visual workflow.
   
###### PNG download
   ```
           // function download(name, uri) {
                var a = document.createElement('a');
                a.download = name;
                a.href = uri;
                document.body.appendChild(a);
                a.addEventListener("click", function(e) {
                  a.parentNode.removeChild(a);
                });
                a.click();
              }

              out$.saveSvg = function(el, name, options) {
                requireDomNode(el);

                options = options || {};
                out$.svgAsDataUri(el, options, function(uri) {
                  download(name, uri);
                });
              }

              out$.saveSvgAsPng = function(el, name, options) {
                requireDomNode(el);

                options = options || {};
                out$.svgAsPngUri(el, options, function(uri) {
                  download(name, uri);
                });
              }
   ```
   
###### Static frame
   ```
   Function drawFrame(styles, mediaFormat, title, subT) {
        // Here we add style.js, unique media variables for each format 
   }
   ```
   
   In my tool project I'm using:
- Save as PNG: https://github.com/exupero/saveSvgAsPng/blob/gh-pages/saveSvgAsPng.js ;
- Static frames: https://github.com/kangax/fabric.js initial idea. However, I've implemented the same system with d3 and        media queries.    
            
## 3 - Implementation
   What we want to add in our chart? Text, labels, axis, annotations, sources, logo!
   The implementation is the stage in which we develop style and chart identity.
   We also decide with which frame we want to work with. And nowadays Frame are really important.
   
- Mobile: 340px x 482px (In my experience, the best w and h for mobile working across most the devices);
- Desktop: 730px x 530px (This variates depending on your article page);
- Social: 560px x 750px (People love scrolling, let's develop in vertical).
- Video: 1920px x 1080px (Yes! Video!)

## 4 - Style

   Styling in css for several charts can be time-consuming. Solution: standardise the structure of the d3.js chart and create    one file - style.js - able to style all your charts, any time. 
   
   ```
var stylemobile = {classes:
[{class:"background {fill: #FDFEFF}"},
{class:"chartholder {fill: none}"},
{class:"title {font: 600 20px/140% 'Lato', sans-serif;fill: #000000;}"}, // etc ...

var styleweb = {classes:
[{class:"background{fill: #FDFEFF}"},
{class:"chartholder{fill: none;}"},
{class:"title{font: 600 26px/140% 'Lato', sans-serif;fill: #000000;}"}, // etc ...
   
var stylesoc = {classes:
[{class:"background{fill: #FDFEFF;}"},
{class:"chartholder{fill: none;}"},
{class:"title{font: 900 34px/140% 'Lato', sans-serif;fill: #000000;}"}, // etc...
   ```

# For your bookmarks and coding time

[Crowbar](http://nytimes.github.io/svg-crowbar/) to download your chart as an SVG. You can then edit it using vector graphics software such as Adobe Illustrator.

[d3-jetpack](https://www.npmjs.com/package/d3-jetpack) for convenience functions that will save you a lot of repetitive typing.

[d3-legend](http://d3-legend.susielu.com/) to make convenient legends based on your scales.

[Textures.js](https://riccardoscalco.github.io/textures/) to use patterns in your visualizations.

[Swoopy drag](https://github.com/1wheel/swoopy-drag) for interactive annotations.

[d3-annotation](http://d3-annotation.susielu.com/) another tool to create annotations.

