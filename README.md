# sass-traject 
## Sass-Traject: A simple, easy-to-use sass mixin that makes your css grid layouts work everywhere 🙌

CSS grid is great, right? Gone are the days of spending countless hours trying to frankenstein a layout together with nothing but floats, inline-elements, popsicle sticks, and crossed-fingers. Now we can just write a few rules and things go _exactly where you'd expect!_ Grid-template-areas even lets you _visually_ get a sneak peek of what your grid will look like, straight in the code. It's really nifty and intuitive: 

```
grid-template-areas: "nav body body"
                     "sidebar body body";
```

Then your client opens their new shiny website in Internet Explorer 11, and all of a sudden, your hard work looks like a crappy 90s website meme. On top of that, it seems like every month, there's a new [article](https://rachelandrew.co.uk/archives/2017/07/04/is-it-really-safe-to-start-using-css-grid-layout/ ) on whether or not it's too soon to start using Grid. The reason? Internet Explorer 11. 

Even though it was released in 2013, Internet Explorer is still [the second most used web browser in the world.](https://netmarketshare.com/browser-market-share.aspx?options=%7B%22filter%22%3A%7B%22%24and%22%3A%5B%7B%22deviceType%22%3A%7B%22%24in%22%3A%5B%22Desktop%2Flaptop%22%5D%7D%7D%5D%7D%2C%22dateLabel%22%3A%22Trend%22%2C%22attributes%22%3A%22share%22%2C%22group%22%3A%22browser%22%2C%22sort%22%3A%7B%22share%22%3A-1%7D%2C%22id%22%3A%22browsersDesktop%22%2C%22dateInterval%22%3A%22Monthly%22%2C%22dateStart%22%3A%222017-10%22%2C%22dateEnd%22%3A%222018-09%22%2C%22segments%22%3A%22-1000%22%7D) We can't tell our clients which browser to use, but **we can adapt** to their pernicious habits.

### Enter: Sass-Traject
Traject(aka sass-traject, aka not-to-be-confused with [this other unrelated repo](https://github.com/traject/traject)) combines two ideas together into an easy-to-read syntax: viewport breakpoints and explicit grids.

### Use
* You need to install and import [include media](https://github.com/eduardoboucas/include-media) into your project
* Once traject.scss has been included in your project, you can do the following syntax:
```
@include traject($childrenObject, $settingsObject);
```
* The `$childrenObject` is a sass map that gathers information about your CSS Grid's children. You can declare this map outside of this mixin call to make your code a little clearer:
```
$newObj: (
  name: 'css-selector',
  secondName: 'another-css-selector'
);

@include traject($newObj, $settingsObject);
```

#### Settings
For the second argmuent of this mixin, we can either pass an array or a map. Using an array will simply apply all rules to all breakpoints:
```
@include traject($boxObj, [
  'sidebar nav nav',
  'sidebar body body'
]);
```
Doing this will create `grid-template-areas` for all modern web-browsers, and the appropriate prefixes to work properly on Internet Explorer( ms-grid-row, ms-grid-column, ms-grid-row-span, ms-grid-column-span), automatically. 

We can take this one step further and specify our css grid layout on certain breakpoints by passing a map instead of an array:
```
 @include traject($boxObj, (
 
  'default': [
    'nav body body',
    'sidebar body body'
  ],

  '<=tablet': [
    'nav body body',
    'nav sidebar sidebar'
  ]

 ));
```
In the example above, we're assigning key-value pairs to declare our grid at specific breakpoints. We can use `'default'` to set up the layout to work outside of a media query, thus the 'default' grid. We then define our `grid-template-areas` as the value.

Immediately after, we're setting up a new grid layout at the `<=tablet` breakpoint. This will override our default settings when we view the page on a smaller screen. 

Using a combination of breakpoints and `grid-template-areas` gives us a lot of power on the front end to set up our grid for every breakpoint and every browser.

#### Modifiers
Modifiers give our layouts a little more control on the fly. They are added to the end of our `grid-template-areas` to modify the layout. *Modifiers always begin with an underscore, `_`*. Example syntax:
```
 @include traject($boxObj, (

  '<=550px': [
    'nav',
    'body',
    '_hide:sidebar'
  ]
  
 ));
 ```
 `_hide:sidebar` is added to the bottom of our `grid-template-areas` array, and will hide the sidebar at this breakpoint. The keyword `sidebar` is extracted from the mixin's first argument, `$childrenObject`.
 
##### _show:child
Targets child, and sets its display css property to `initial` (`block` on IE). 
ie: `_show:body`

##### _hide:child
Targets child, and sets its display css property to `none`. 
ie: `_hide:nav`

##### _templateRows, _trrows, or _tr
Uses the grid-template-rows property and assigns it to the grid.
ie: `_templateRows: repeat(auto-fit, 186px)`

##### _templateColumns, _tcolumns, or _tc
Uses the grid-template-columns property and assigns it to the grid.
ie: `_tr: 200px 1fr 1fr`

