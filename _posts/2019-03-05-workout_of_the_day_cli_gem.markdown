---
layout: post
title:      "Workout of the Day CLI Gem"
date:       2019-03-05 22:25:13 -0500
permalink:  workout_of_the_day_cli_gem
---


Embarking on my first solo project has been a great experience so far! There's nothing like staring at that blank screen to make you feel both intimidated and excited at the same time.

## Brainstorming
I started out the project brainstorming website data that could be useful to pull down for a user and parse into the relevant chunks of content. As a lawyer, my first thought was to pull legal content. After striking out on my state's court website and the state revisor of statutes website due to /robots.txt file restrictions, I remembered my days as a real estate attorney fresh out of law school researching local ordinances for land use cases. Finding the ordinances of small, or even larger, cities could sometimes be challenging. I remembered a website, [library.municode.com](https://library.municode.com/) that compiled local ordinances from around the country and decided this might be a fun place to start.
 
##  False Start (& learning new tools!)
I was a little worried about how fancy the site looked, and after my CLI prep meeting, my worries were confirmed when the instructor said the site was loaded with javascript. This meant I couldn't use standard data scraping techniques and tools. I was up for the challenge, though, and the instructor sent along helpful resources to get me started ([Poltergeist](https://readysteadycode.com/howto-scrape-websites-with-ruby-and-poltergeist) and [PhantomJS](https://www.simon-neutert.de/2017/scrape-js-powered-websites-with-ruby-and-selenium/)). Soon though, she noticed that PhantomJS was incompatible with the latest MacOS update, Mojave, and sent along a new tool, [Waitr](http://watir.com/), with a link to a github demo she had created!
 
Waitr was really interesting to read up on and experiment with. It uses headless Chrome, which essentially opens a browser in the background, without any user interface. This lets you load the page and then scrape the rendered html, getting around the hurdles javascript creates for standard scraping! I spent a couple hours playing with the instructor's demo and reading plenty of tutorials and stackoverflow threads but could not get the demo working on my machine. Despite downloading headless Chrome, editing my $PATH, and trying numerous other approaches, each time I ran the program I got the same error: Cannot find Chrome binary. 

When I initially decided to explore this more complicated form of scraping, I made a deal with myself that I wouldn't go too deep down the rabbit hole at the expense of losing focus of the assignment objective: writing DRY Object-Oriented Ruby code. When I hit the 2-hour exploratory limit I had set for myself, I cut my losses and went back to the drawing board.

## Bulding a CLI Gem!
My next attempt was much more successful! After getting back from the gym, I was ready to start my gem, and got to thinking about how one of the hardest things for me when I don't have a gym membership is coming up with what workout I want to do on any given day. With that thought, I began searching websites that offered daily workouts. I came across three sites that posted workouts updated daily, and one site with long lists of different categories of bodyweight workouts. After exploring parsing the html on each site with a [Repl.it tool](https://repl.it/repls/MerryIllAxis), I decided to proceed with my workout of the day CLI Gem.

After watching video walkthroughs of building the [Daily Deal Gem](https://www.youtube.com/watch?v=_lDExWIhYKI)  and [creating a new project in the Learn IDE](https://www.youtube.com/watch?v=_lDExWIhYKI), I was on a roll. I started with my CLI interface, feeding in static data to get the basic flow, then moved to the Workout class, and finally, to the Scraper class. After floundering through my initial attempts at scraping javascript sites, it felt good to get back to the concepts that are the focus of the project.

My Workout of the Day Gem scrapes four websites, using a variety of techniques. Two of the websites list their daily website on the homepage, and then take users to a second page for details on the workout. The scraper methods for these sites pull title and url information from the homepage, and then use the url to scrape the description from the secondary page. Two of the sites include multiple workouts, so for these, I iterate over the page elements to pull the details of each workout. Because the bodyweight website doesn't provide a daily workout, the scraper instead chooses a random workout from each category of workout listed on the page. When a new object is instantiated from my Scraper class, all four website scraper methods are called.  

In each of my scraper methods, the details scraped from each website instantiate a new workout object from my Workout class. The Workout class saves all newly instantiated Workout objects to a class variable. My CLI class uses the Workout class variable to pull information about the workouts and present it in a user-friendly manner. For a full description of the user interface, see my [video walkthrough](https://drive.google.com/open?id=1pFTuasQZCnFRQjQx1LoXbvTPsPhb7fy0).

After getting a working model done during the first day on the project, I spent the next two days refining the flow and formatting and refactoring the code. Just like the grant application I worte at work recently, getting a draft down on figurative paper is always the most challenging step. Once you have something to work from, the work becomes much more manageable. Once I had a product I though was ready for testing, I brought in my spouse who has no patience with technology and is therefore an excellent user tester. She gave great feedback and within seconds discovered issues with my error message CLI flow. After a few more tweaks I felt I had a project I was ready to submit. 

## Takeaways
The CLI Gem project has been a great learning experience. It's reinforced my understanding of Object-Oriented Ruby and given me a chance to experiment with techniques like Regex and .gsub that I was familiar with but hadn't spent as much time working with. Taking the project step-by-step helped the process feel manageable, and google remained my friend throughout, especially in providing guidance on pesky formatting issues. 

I'm excited (and nervous!) for my Project Review. Despite the time I've spent refactoring my code, I know I'll learn from that process and discover new ways to write more elegant code and continue my coding journey.
