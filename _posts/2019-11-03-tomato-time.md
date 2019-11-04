---
layout: post
title: Tomato Time
date: 2019-11-03 22:59 -0700
---

During the snowy days in mid-October in 2019, I had a chance to work on a group project called [Tomato Time](https://peaceful-chamber-62417.herokuapp.com/). It left me with strong feelings in that I drew a conclusion that it deserved a blog post.

So here you go.

#### Design Patterns
- The project involved four people. A team of 4 meant that it naturally amoeba-ed into 2 sub-teams:
  - Building a Sinatra app that concerns with designing internal API and backend operations
  - Building an engaging UI

  This separation of concerns not only allowed us to work in pairs but also made it easy to refactor the app. One team could be dedicated to storing and computing data; the other team could focus on making the app as engaging and aesthetically pleasing as possible, like so:

  ![running-tomato](https://thumbs.gfycat.com/BriskLankyCopperhead-size_restricted.gif)

  I was responsible for the first part, building a sinatra app that would consume an external API, format the response, and build an internal api out of it. Let me tell you, that I was in visceral pain with having to configure literally everything from scratch. Especially, it gave me a hard time asking me to figure out how to compose a `travis.yml` file for continuous integration and which gems to require for certain files. All of which I took for granted in a Rails app without a second thought. In hindsight though, this mildly agonizing experience taught me the most about web development in RoR.


#### Implementation choices
The project culminated the learning goals of the current module. It allowed us to synthesize what we'd been learning and make judicious choices under some constraints and assumptions. Not an exhaustive list, but this is a list of things that we are able to do now:

- Set up Google OAuth 2.0 for user authentication
- Set up continuous integration (CI) for automatic build and deployment
- Send email from a Rails app with SendGrid
- Implement a background worker (ActiveJob) to optimize the app
- Implement a cron job to schedule a time-based task running in the background (i.e., sending out an email at a specified time period)
- Measure app performance (aka, response time per endpoint) with Skylight
- Implement a text-to-speech functionality with a JavaScript library called ResponsiveJS


#### Decent practices
- Planning stage: We conducted a series of brief meetings for about 2 hours on Day 1 of our project. Guided by this [meeting template](https://backend.turing.io/module3/projects/materials/terrificus_meeting_schedule), we took the following steps:
  - Brainstorm the most important features that we would like to build in our project.
  - Define a minimum viable product (MVP).
  - Build wireframes with Balsamiq to simulate user experience.
  - Churn out / chunk out user stories.
  - Design a tentative schema with LucidChart.
  - Consider possible architectural choices, regarding background workers, caching, and JavaScript.

- Execution stage: For each user story, we took a solo-spike-first approach in which individual members conducted research on their own and played around with new technologies before convening in pair programming. This way, we had something to work on together and made the best use of the group time.

- Checkpoint stage: Our team was supervised by a project manager (aka, one of our instructors). Regular check-ins gave us a chance to share our team progress, recent achievements, and current bottlenecks. First and foremost, these sessions provided insight into the art of prioritizing. There were some features that we wished we could impart on our app. For instance, we wanted to build an interactive, multi-player game app. But this cool feature required some familiarity with Action Cable, which was beyond my understanding at that point. The time-bound project demanded that we build a robust MVP first, and push this desirable feature under the "Future Iterations" category. Thankfully, the intermission week is approaching, so I can look into these features in more detail during break. 
