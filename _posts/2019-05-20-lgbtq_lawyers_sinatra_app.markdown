---
layout: post
title:      "LGBTQ Lawyers Sinatra App"
date:       2019-05-20 01:05:57 -0400
permalink:  lgbtq_lawyers_sinatra_app
---

## Beginnings
As I worked through the Sinatra unit, an idea for the final project simmering in my mind, based on some volunteer work I do with an LGBTQ legal clinic. In the clinic, volunteer lawyers meet with LGBTQ folks for 15-20 minutes on a variety of legal issues. When a client needs more assistance than the clinic can provide, the other lawyers and I need to give the client a list of referrals. However, while we may know lawyers who practice in a given area of law, we don't always know whether those lawyers have LGBTQ competence. In an effort to make sure we don't send a client to a place where they might be misgendered or made to feel unwelcome, we currently send out an informal call to the clinic volunteers and others in our networks for any LGBTQ-friendly lawyers who could handle a certain case type. This method is inefficient and leads to an incomplete list of competent lawyers. 

This app is a starting point to filling that need by creating a database of lawyers with LGBTQ competence. Verified users can add to the database of lawyers and see which lawyers have been added.

## [The App](https://github.com/jei-doubleton/lgbtq-lawyers-sinatra-app)
The app is a fairly straightforward MVC. There are four models: `User`, `Lawyer`, `PracticeArea`, and `LawyerPracticeArea`, with the following associations:
* a User `has_many` Lawyers,
* a PracticeArea `has_many` LawyerPracticeAreas, and `has_many` Lawyers, through LawyerPracticeAreas
* a Lawyer `belongs_to` a User, `has_many` LawyerPracticeArea, and `has_many` PracticeAreas, through LawyerPracticeAreas
* a LawyerPracticeArea `belongs_to` a Lawyer and a PracticeArea

The app has 3 controllers, an `application_controller`, a `lawyers_controller`, and a `users_controller`. The `users_controller` and accompanying views allow users to signup, login, and view their profile page, which lists all lawyers a user has added. The `lawyers_controller` and views allow users to create new lawyer entries, view existing lawyer entries, edit users' lawyer submissions, and delete users' lawyer submissions. 

User submissions are validated in a number of ways. Usernames and user emails must be unique, as do lawyer and practice_area names. If a user attempts to submit a duplicate, the app presents a flash message explaining the error. Flash messages are also used if the user attempts to access a page that is forbidden, such as the list of lawyers if they are not logged in, or the edit page for a lawyer belonging to another user.

## The Process
I found creating the app to be a fairly smooth process. I completed the bulk of my app in 1-2 hour chunks of work, which allowed me to focus on discrete pieces of the app without being overwhelmed by creating a web app from scratch. I started by sketching out the core features of the app in a notes file, answering three questions:
1. What core functionality did my app need to have?
2. What tables did I need to achieve that functionality? 
3. How would my tables/models relate to each other? 

I used this notes file to guide me in creating first my migrations, and then my models. This was incredibly useful as once I had created the overall architecture it was just a matter of translating my words into code, which allowed me to first focus exclusively on architecture, and then focus exclusively on the code itself. I then created some seed data and verified that everything was working as expected via `tux`.

To create my controllers and views I followed the path a user would take when first encountering my website, focusing on each discrete action/view without worrying too much about the others. This worked well to naturally make sure most dependencies fell into place, such as needing a logged in user to create a lawyer, and needing an existing lawyer to edit a lawyer.

After creating my basic layout view, I created the signup and login forms (and logout form/link). I then sketched out a very basic user show page (e.g., "My Profile") that would show all lawyers added by a user.  Once these basic user controllers were working, I moved on to my lawyer CRUD actions - creating a lawyer, viewing an individual lawyer and list of all lawyers, updating a lawyer entry, and finally, deleting a lawyer.

With all these discrete pieces in place, I moved onto connecting everything. Wherever a lawyer listing showed up, I added edit and delete buttons if the lawyer belonged to the user. Whenever I wanted a page restricted to logged in users, I added `logged_in?` logic, redirects and flash messages. 

With everything in place, I played around with the app, noticing a few bugs, such as that editing a lawyer caused that lawyer's practice areas to pile up, since they were being added without clearing the existing practice areas. This ad hoc testing made me really appreciate test-driven development, and for my next project, I'll take the time to write tests so that I can systematically catch issues such as the duplicate practice areas.

## Next Steps
Now that I have an app that (I hope!) meets the project requirements, I'd like to add in at least two additional features to get it closer to a truly useful website. First, I'd like to add some basic design, perhaps using bootstrap. As my partner quipped, without any formatting, the site is currently very Craigslist chic. Second, I'd like to add some filtering capabilities. Even with 10 test entries I can see how it would be difficult to find a list of lawyers to provide as referrals, and this problem would only increase as more lawyers were added. Therefore, I'd like to experiment with adding what will essentially be a search form that will query the database and return matching lawyers.

It's been so cool to know that I can build something from database to user view, and I'm excited to continue on the journey!

