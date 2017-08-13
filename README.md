## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository and inspect the code.

## Student's Notes

To open the webpage follow these simple steps. Running through [ngrok](https://ngrok.com/) will allow testing through Google PageSpeed Insights

1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

  ### Part One: Optimizing index.html

  By making the following adjustments to the homepage a Google PageSpeed Insights score of **Mobile - 93 / Desktop -95** was achieved.

  ######Images
  -Passed all images through ImageOptim compression.
  -Copied pizzaria.img over to the img folder in the root and made it 100px(per the html settings) and compressed it. Renamed it pizzaria_icon and routed the html to pull this image.
  -Moved all images from the server (2048!/web-pref/mobile) and moved them to the img folder, resized and compressed.

  ######Script tags
  -Removed google fonts and used sans-serif.
  -Made the google analytics script async. to stop render blocking.
  -Minified both styles.css and print.css.
  -Inlined minified styles.css for quick rendering.

  These changes allowed all images to be pulled from the same source and allowed them to be sized from specification and compressed, no bytes wasted. Scripting changes were mostly to stream-line rendering.


  ### Part Two: Optimizing main.js

  Through the following tweeks the Pizzaria page was able to achieve a **resize time between .245 - .319** and an **average frame rate of 60** on the laptop setting in google developer.

  ######LN 402: resizePizzas Function

  -Removed determineDX function and moved switch function and changePizzaSizes under changeSlider function. This combined 2 switch loops to one since they had the same switch values, both outputs could be accomplished in one loop.

  ######LN 479: function updatePositions

  -Moved `var items = document.getElementsByClassName('mover');` outside the function. *This only needs to run once, so it is now placed as global variable.*
  -Created a sctop and remainderArray var. *sctop only needs to be pullled at the function level, not each time in the for loop. remainderArray, i%5 only produces five possible numbers, so we can create a for loop that runs the minimum possible times and pushes it in the array.*
  -The above changes allowed me to strip the original for loop down to basics. removing the phase variable.
  -Changed from `items[i].style.left` to `items[i].style.transform`for performance reasons.

  ######LN 511: function sliding pizza generator

  -Due to transformation added `elem.style.left`on line 523.`elem.style.willChange` on line 524. *this sets an initial px value for the transform to calculate off of.*
  -Changed the for loop i< to 56. *which is the needed amount of pizzas to fill a 2200x1048 screen.*
  -changed source image on line 519 so that it is the same size called out. 100x73px.
