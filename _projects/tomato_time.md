---
layout: project
title:  "Tomato Time"
description: "Group Project"
link: "https://github.com/joshsherwood1/tomato_time_project"
image: "https://alumni.turing.io/sites/default/files/styles/project_screenshot/public/project_screenshots/tomato_time_final.png?itok=wVymuVTf"
---
[Visit website](https://peaceful-chamber-62417.herokuapp.com/)

<hr>

#### Description
In this group project, my team built an interactive trivia app with Rails. Users can make customized games by specifying the category, level of difficulty, and amount of questions for each game. The following list describes what we were able to accomplish in this project:

- Set up Google OAuth 2.0 for user authentication
- Set up continuous integration (CI) for automatic build and deployment
- Send email from a Rails app with SendGrid
- Implement a background worker (ActiveJob) to optimize the app
- Implement a cron job to schedule a time-based task running in the background (i.e., sending out an email at a specified time period)
- Measure app performance (aka, response time per endpoint) with Skylight
- Implement a text-to-speech functionality with a JavaScript library called ResponsiveJS to have each question narrated to the user

My main responsibility involved two tasks: building a Sinatra app that consumes an external API from the Open Trivia Database and generates endpoints for the main app (Tomato Time) to consume; and implementing a text-to-speech (TTS) functionality for question contents within each game.
