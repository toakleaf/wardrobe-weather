# Wardrobe Weather

Aren't all weather apps really just wardrobe planning apps anyways?

[Live Demo!](https://weather-wardrobe.netlify.com/)
![screenshot](/screenshots/screenshot.jpg?raw=true)

## My process

For a job interview I was given an assignment to create a "weather widget." As I'm currently building out a portfolio, I thought it might be neat to give a blow-by-blow accounting of my development process on this simple little app, along with the elapsed time to perform each task. That's the goal anyways, we'll see how it turns out in the end.

## The project:

Part of the reason I've gravitated toward programming is because I am the living embodiment of DRY practices. In my day-to-day I try to avoid doing any task that might also be included in the activities brochure for an eternal damnation, and as such Sisyphus's plight is never far from mind. Therefore, whenever confronted with mundane work I have a sometimes regrettable habit of trying to wring out a drop of dignity in purpose where there might be precious little. Sometimes it leads nowhere and I end up just pushing that same rock up the hill as everyone else. Other times, after asking a series of Jack Handy-esque, like "what is a weather widget, and why would anyone use it?" I end up in interesting places. This is one of those other times.

## Monday:

Was given project parameters attached below. Have a busy week planned, so I informed recipient that I won't be completing project until weekend. Will use time to mull over ideas that could make this more interesting than surface requirements. For this particular project it should be easy enough to scale back later and revert to status quo concept.

## Saturday 9:30 pm:

Wow this weeks sucked. Anyways, have a bit of time now to spend thinking about this and getting organized. My basic concept for this project is drawn on two primary inspirations:

1. All weather apps are really just clothing selection apps

2. My wife has spent the last two days helping plan her sister's wedding by doodling dress ideas

What I came up with was an idea for a "paper doll" style app that would pull together an svg image of an outfit based on weather forecast conditions.

So my wife and I sat down and made the following chart of temperatures and conditions and what she would wear in each scenario. (15 min)

![weather clothing chart](/screenshots/chart.jpg?raw=true)

I then commissioned her to sketch out on tracing paper each clothing item on top of a paper doll template. (1 hr)

![clothing sketches](/screenshots/tracings.jpg?raw=true)

While she was sketching I went and did more research on the [Open Weather API](https://openweathermap.org/appid). (15 min) And then fired up a github repo and initiated a new vue project for this. (15 min) I contemplated creating the project in react or svelte, and I might still create versions of it in those later, but this particular project is for a vue shop, so I might as well do as the Romans here.

My final act of the night was to sit down and start writing this readme. I tend to take way too much pride in my writing and so it ended up being my lengthiest contribution of the night. (1 hr).

Total elapsed work time:

Me: 1.5 hrs

Wife: 1 hr

## Sunday 8:00 am:

I wake up and begin by doing more writing on this readme. (45 min)

I start my day by thinking a bit about architecture and trade offs. The primary trade off here is that I don't want to build my own server-side API for this project. If I were making more than a cute little demo app I would feel differently, but I'm not.

#### Security:

This project specified the use of the [Open Weather API](https://openweathermap.org/appid) which requires the developer to register for a private api key to make the GET requests necessary to gather information critical to the application. There is simply no good way to secure this private key in a strictly client-side piece of coding. I'm going to be creating a netlify demo of this app, and so I will be able to easily employ an environment variable to at least keep the key off github, however, anyone with the ability to use dev tools in a browser will still be able to get the key when using my live demo. For this demo project I'm ok with this vulnerability, as the worst that can happen is someone skims my key and my account at Open Weather gets suspended. If I were using an API where I was being charged for usage then I would be forced to wrap the functionality of the Open Weather API in my own API server, so that I would be making all requests to Open Weather server-side and not exposing my key at all.

In the API, if your key gets suspended you get the following json response:

```
{
"cod": 429,
"message": "Your account is temporary blocked due to exceeding of requests limitation of your subscription type.
Please choose the proper subscription http://openweathermap.org/price"
}
```

#### Location:

Another part of the project specification was to have the app populate results based on browser location, as well as manual location entry. Browser location is easy, as it merely requires a simple [Geolocation](https://www.w3schools.com/html/html5_geolocation.asp) call. However, the Open Weather API specifies two different end points for lat/long coords and city names, so that must be dealt with.

Whenever possible I also like to offer live-search autocomplete drop downs to help users correct their spelling and understand their options. As the Open Weather API doesn't really have any solutions for this built in, to implement such a feature I would again need to be creating a API server to wrap the searching of their [city list](http://bulk.openweathermap.org/sample/), as it is way too much data to simply stuff in a client-side app. As it stands users will need to precisely type the city name and optionally the country code, commas separated, into a search field and then manually submit the form to make a request. I could do some regular expression matching to clean up the user input before submitting to the API, however such effort would really be better spent on an actual solution like implementing a live-search. In for a penny, in for a pound, and therefore I'm forgoing spending a single cent putting lipstick on this search issue.

## Sunday 9:45 am

Time to fire up illustrator and SVG-ify these sketches.

## Sunday 12:00 pm

Break

## Sunday 1:00 pm

Back to creating SVG files from sketches while half watching some football. I'm having to modify the SVG tracings quite a bit to get everything to work together, but the finished artwork is looking amazing in my opinion. I also added a model, which I was originally planning to exclude, but it adds a good bit to the finished product.

## Sunday 5:30 pm

Finally finished all the artwork!!

Break

## Sunday 6:30 pm

Started coding in vue app. Decided that because there are so many different SVG groups, I will break SVG up as if it were a bunch of html and componentize all of the groups so they can be loaded dynamically based on props passed into main component.

## Sunday 7:15 pm

Breaking up that SVG into components was incredibly repetitive and took about 45 minutes. Taking another short break now.

## Sunday 7:30 pm

Adding all of the conditionals into the Wardrobe.vue file so that SVG changes dynamically based on props.

## Sunday 8:00 pm

Dinner break.

## Sunday 9:30 pm

Had to fix a few things in the artwork so background colors didn't bleed through. (20 min)
Spent way too long getting Vue CLI's environment variables set up. Forgot that you needed to prefix everything with "VUE*APP*" (20 min)
Hooking up all the color props also took a long time. (20 min)

## Sunday 10:45 pm

Finally ready to start fetching info from the API. Data seems to be coming in just fine. Loads weather data perfectly based on browser Geolocation. Wrote some quick scripts to process it so that forecast is averaged over 6 hours, which I thought best for this use case. I've also been continually fixing some bugs with the artwork which has taken some additional time.

## Monday 12:15 am

Everything is working. Just need to add the search bar and weather info. Going to bed and will knock it out in the AM.

## Monday 9:30 am

Did some styling. Began working on info pane. Should be quick now.

## Monday 11:00 am

App is finished, just cleaning up files and adding a background transition so it's not so jarring.

# Total time spent on project:

(while working at a leisurely pace)

Artwork: 10 hrs

Documentation/deployment: 2.5 hrs

Coding: 5 hrs
