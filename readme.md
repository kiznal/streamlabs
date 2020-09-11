## Intro

This is a project that contains the code that I used to generate my Twitch  subscriber alerts, which emulates the Exclamation Mark Blocks from Super Mario 3D World and Super Mario Maker 2. I'm no pro at HTML/CSS/JS so it'll be a nasty mix of good and bad practices. It seems to work well though.

I wouldn't have been able to get these alerts working without this blog post: https://medium.com/@devinwl/tribulations-on-adding-custom-twitch-alerts-to-streamlabs-4130438b8787. It explains a lot of the weird CSS that you need to be aware of and override to get your stuff to line up correctly.


# subscription.html

This just contains a single font reference and the basic structure for the alert. Below I'll list the fields that I found and/or used to access the settings that you fill out in the StreamLabs alert menu. If you mess around with alert settings and observe the html in the dev menu in your browser, you could probably find a few more, but I didn't do search for more than the few that I needed. These were right last time I checked, they are subject to change.

- {name} - username of the subscriber
- {messageTemplate} - the entire message that displays (i.e. "{user} just resubscribed for {months} months!")
- {userMessage} - the resub message that the user inputs
- {img} - the image that you can upload from the StreamLabs menu
- {months} - the amount of resub months. I think this is 0 on a first-time sub?


# subscription.css

Not a lot to say here. The CSS will probably vary wildly depending on your HTML/JavaScript needs. I ended up just using !important for a ton of fields to get them to work. Seems as though there's hidden CSS somewhere in the StreamLabs page that you just need to override. 

I wanted to have most things aligned in the center/middle and display to be block or none. Eventually I left some of the alignment to the JavaScript to just be calculated from the viewwidth because I just couldn't get the CSS to work. 


# subscription.js

This is where the real fun begins. I'll go over the two big nuances that I came across first, then explain what I was doing in my code.

1. You can't use global variables or else you get a "has already been declared" error after the first time the alert triggers. I have no clue why this is, I'm no JavaScript insertion master, but that's what happens. So to utilize const variables, just make functions for it.

2. Loading in pictures other than the {img} sometimes has noticeable delay, like using imgur links or something. To get around this, I converted some pictures to base64 and included them within the code itself (the last function with the super long lines). These always loaded consistently for me.

With those two things in mind, I primarily used the GreenSock Animation Package (gsap) to animate the alerts. Since you can't really include libraries, I took the advice from the blog post above and included a minimized version of gsap as a single line at the top of this file in order to utilize the animation properties. Other than that, it was just a bunch of animation code. Not a lot more to explain.


## Setup

Right before committing this, I pasted the HTML, CSS, and JS files into their respective boxes into the StreamLabs custom code fields and verified that they worked. I seemed to have trouble with getting the custom code workg in the Resub alert, so I did a custom sub month alert for 2 or greater months and the code seemed to work in there.

That's it. Hope this is helpful to anyone who sees it.