---
layout: post
title: Hello Turing
date: 2020-01-18 13:05 -0700
---
My coding journey began in the summer of 2019. Since then, I have had the opportunity to work with interesting people on a variety of projects. Having no idea what would unfold in the better part of the last year, I signed up for the backend program in Turing School of Software and Design. Now having crossed the finish line, I am cooling down a bit this weekend and spend some time reflecting on what happened.

While subjective experiences may vary for each student at Turing, there is a curriculum that emboldens every student to keep learning. I appreciate those behind the scene constantly working on delivering a better learning experience for students. Below I have described the program structure to the best of my ability.

As shown in the diagram, both frontend and backend programs consist of 4 modules. In each module, which lasts for 6 weeks (or 30 school days), students get to work on 4 different projects, two weeks per project. Weekly check-ins with an instructor, learning goals and rubric are provided to guide project development and evaluate the final outcome. Between modules, students are given an intermission week, in which they take a break from work as well as completing prework for the next step (denoted as a red button).

<img src="https://user-images.githubusercontent.com/24424825/72669787-3b1fd700-39f3-11ea-9181-0cb1d7c56c45.png" width="60%" style="display:block; margin-left:auto; margin-right:auto;">

There are two independent projects, at the beginning of the mod and at the end of the mod. The first solo project is not graded; it is for students to get their feet wet and play around with new ideas and tools. In a pair project, two students work in pairs and follow the agile process, initiating the project with a DTR and exiting with a retro. In a group project, three to four students work on a larger-scale project with advanced requirements, following the agile process. In the final independent project, students get to work on their own again, now being equipped with a better understanding of concepts and tools covered in this module. Lastly, each student is required to deliver a short portfolio presentation to the instructor to talk about their progress and identify room for improvement for the next module.

Below is the same idea outlining the module structure at Turing, expressed in Ruby:

```ruby
projects = ['solo', 'pair', 'group', 'solo']
4.times do |mod|
  puts "Module #{mod+1}"
	projects.each_with_index do |project, i|
	  puts "Week #{i+1}: " + project + ' project'
	end
  if mod == 3
    puts '---------------------------'
    puts 'Happy graduation!'
  else
    puts '---------------------------'
    puts 'Intermission week: prework'
    puts '---------------------------'
  end
end
```
