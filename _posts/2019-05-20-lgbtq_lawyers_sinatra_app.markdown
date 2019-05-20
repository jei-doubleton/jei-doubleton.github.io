---
layout: post
title:      "LGBTQ Lawyers Sinatra App"
date:       2019-05-20 05:05:57 +0000
permalink:  lgbtq_lawyers_sinatra_app
---

## Begining
My idea for the Sinatra final project had been simmering in mind as I worked through the Sinatra unit. For the past several years, I have been volunteering with an LGBTQ legal clinic. Volunteer lawyers meet with LGBTQ folks for 15-20 on a variety of legal issues. One of the struggles for the other volunteer lawyers and me has been when the client needs more legal advice than the clinic can provide, and therefore needs a referral to a lawyer for full representation. It is particularly important that we know the degree of LGBTQ-competency of the lawyers we refer the client to, so that we can adequately prepare our clients.

## The App
The app is a fairly straightforward MVC. There are four models: `User`, `Lawyer`, `PracticeArea`, and `LawyerPracticeArea`, with the following associations:
* a User `has_many` Lawyers,
* a PracticeArea `has_many` LawyerPracticeAreas
* a PracticeArea `has_many` Lawyers, through LawyerPracticeAreas
* a Lawyer `has_many` LawyerPracticeArea
* a Lawyer `has_many` PracticeAreas, through LawyerPracticeAreas

The app has 3 controllers, an `application_controller`, a `lawyers_controller`, and a `users_controller`. The `users_controller` controllers user signup, login, and show views, while the `lawyers_controller` allows users to create new lawyer entries, view existing lawyer entries, edit users' lawyer submissions, and delete users' lawyer submissions. The accompanying views allow users to interact with the website by submitting forms (to sign up, login, create lawyers, edit lawyers, and delete lawyers). 

User submissions are validated in a number of ways. Usernames and user emails must be unique, as do lawyer and practice_area names. If a user attempts to submit a duplicate, the app presents a flash message explaining the error. Flash messages are also used if the user attempts to access a page that is forbidden, such as the list of lawyers if they are not logged in, or the edit page for a lawyer belonging to another user.

## The Process
I found creating the app to be a fairly smooth process. I completing the bulk of my app in the evenings after work, in 1-2 hour chunks of work. I started by sketching the core features of the app in a notes file and using that to create my migrations, and then models. Once I had my models and associations working, which I verified via `tux` and creating some seed data, I moved onto the controllers and views. Each evening I would focus on completing a discrete section. For example, I completed my signup form one evening, and the next evening focused on creating a login form, and then new lawyer form. Taking the project chunk by chunk made the prospect of creating a website from scratch much less intimidating!
## Next Steps
Now that I have my MVP, the two next features I'd like to add to my Sinatra app are some basic design, perhaps using bootstrap, and filtering capabilities. To have a truly useful website, users would need to be able to quickly sort through lawyers by practice area at a minimum, so I'd like to explore how to bring that functionality to life.


