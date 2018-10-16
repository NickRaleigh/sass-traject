# sass-traject 
![alt text](http://nickraleigh.com/wp-content/uploads/2018/10/logo.png)
## Traject: A simple, easy-to-use sass mixin that makes your css grid layouts work everywhere 🙌

CSS grid is great, right? Gone are the days of spending countless hours trying to frankenstein a layout together with nothing but floats, inline-elements, popsicle sticks, and crossed-fingers. Now we can just write a few rules and things go _exactly where you'd expect!_ Grid-template-areas even lets you _visually_ get a sneak peek of what your grid will look like, straight in the code. It's really nifty and intuitive: 

```
grid-template-areas: "nav body body"
                     "sidebar body body";
```

Then your client opens their new shiny website in Internet Explorer 11, and all of a sudden, your hard work looks like a crappy 90s website meme. On top of that, it seems like every month, there's a new [article](https://rachelandrew.co.uk/archives/2017/07/04/is-it-really-safe-to-start-using-css-grid-layout/ ) on whether or not it's too soon to start using Grid. The reason? Internet Explorer 11. 

Even though it was released in 2013, Internet Explorer is still [the second most used web browser in the world.](https://netmarketshare.com/browser-market-share.aspx?options=%7B%22filter%22%3A%7B%22%24and%22%3A%5B%7B%22deviceType%22%3A%7B%22%24in%22%3A%5B%22Desktop%2Flaptop%22%5D%7D%7D%5D%7D%2C%22dateLabel%22%3A%22Trend%22%2C%22attributes%22%3A%22share%22%2C%22group%22%3A%22browser%22%2C%22sort%22%3A%7B%22share%22%3A-1%7D%2C%22id%22%3A%22browsersDesktop%22%2C%22dateInterval%22%3A%22Monthly%22%2C%22dateStart%22%3A%222017-10%22%2C%22dateEnd%22%3A%222018-09%22%2C%22segments%22%3A%22-1000%22%7D) We can't tell our clients which browser to use, but **we can adapt** to their pernicious habits.

### Enter: Traject
Traject(aka sass-traject, aka not-to-be-confused with [this other unrelated repo](https://github.com/traject/traject)) combines two ideas together into an easy-to-read syntax: viewport breakpoints and explicit grids.
