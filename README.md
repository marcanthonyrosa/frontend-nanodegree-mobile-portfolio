# Udacity's Website Optimization Project

## Overview
The goal of this project was to optimize a sample online portfolio for speed and performance considerations! Thanks to the learnings of Udacity's [Website Optimization](https://classroom.udacity.com/nanodegrees/nd001/syllabus?activePartKey=00113454012) course, I applied various optimizations to the pixel pipeline around JavaScript, Styles and Layouts, and Compositing and Painting considerations.


## Installation

You can access the website live here at [marcrosa.me/optimzations](http://marcrosa.me/optimizations/).

Or, to run this project locally, try the following steps:

1. Fork or download the repository from my project repository @  [github.com/marcanthonyrosa](https://github.com/marcanthonyrosa/frontend-nanodegree-mobile-portfolio)
2. Open index.html file from a browser

3. To inspect the site on your phone, you can run a local server

```bash
$> cd/path-to-your-project-folder
$> python -m SimpleHTTPServer 8080
```

3. Open a browser and visit localhost:8080
4. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

``` bash
$> cd /path/to/your-project-folder
$> ./ngrok http 8080
```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

## Ojectives and Implementation

#### Part 1: Optimize PageSpeed Insights score for index.html

Objective: `index.html` achieves a PageSpeed score of at least 90 for Mobile and Desktop.

Solutions:
- Denoted two JS files as "async" to reduce the critical rendering path length
- Eliminated unused fonts and CSS properties
- Compressed and resized the pizzaria image
- Minified CSS and included it in `index.html` to reduce total resources requested

Outcome: [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fmarcrosa.me%2Foptimizations) shows:
- Mobile: 95/100 Speed; 100/100 user experience
- Desktop: 97/100

Woohoo!


#### Part 2: Optimize Frames per Second in pizza.html

Objectives:
1. Optimizations made to `views/js/main.js` make `views/pizza.html` render with a consistent frame-rate at 60fps when scrolling.
2. Time to resize pizzas is less than 5 ms using the pizza size slider on the `views/pizza.html` page. Resize time is shown in the browser developer tools.

Solutions:

**1. For 60fps scrolling**:
- Reduced the number of pizzas being generated (from 200 to 35!) to eliminate excess rendering that's not viewable in the view
- I moved the value of phaseScrollTop to its own variable **outside the loop** so that the loop wouldn't have to create and reference it each instance (which saved a lot of resources!)
- Since there were only 5 phase calculations being used, I moved these into an array instead of being generated on the fly
- Replaced the method ``style.left`` with ``transform = translateX``
- Used requestAnimationFrame when calling UpdatePositions to improve frame rate

**2. For resize pizzas < 5ms**:
- Completely refactored the function resizePizzas to remove a number of expensive functions and inefficient calculations (ex: ``determineDx``), and replaced them with a function that sets pizzaContainerSize to a percentage width depending on the slider position
- Reduced the number of instances the DOM was accessed and organized those instances as variables outside loops
- leaned on more efficient methods like getElementByClassName instead of expensive methods like querySelectorAll

Outcome:
1. Average scripting time to generate last 10 frames: 0.2095 ms
2. Time to resize pizzas: 0.4849 ms

Woohoo!!

## License

MIT License

Copyright (c) [year] [fullname]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
