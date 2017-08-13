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

  By making the following adjustments to the homepage a Google PageSpeed Insights score of [x] Mobile - 93 / Desktop -95 was achieved.

  #####Images
  -Passed all images through ImageOptim compression.
  -Copied pizzaria.img over to the img folder in the root and made it 100px(per the html settings) and compressed it. Renamed it pizzaria_icon and routed the html to pull this image.
  -Moved all images from the server (2048!/web-pref/mobile) and moved them to the img folder, resized and compressed.

  #####Script tags
  -Removed google fonts and used sans-serif.
  -Made the google analytics script async. to stop render blocking.
  -Minified both styles.css and print.css.
  -Inlined minified styles.css for quick rendering.

  These changes allowed all images to be pulled from the same source and allowed them to be sized from specification and compressed, no bytes wasted. Scripting changes were mostly to stream-line rendering.
  

  ### Part Two: Optimizing main.js

  Through the following tweeks the Pizzaria page was able to achieve a [x] resize time between .245 - .319 and an [x] average frame rate of 60 on the laptop setting in google developer.
