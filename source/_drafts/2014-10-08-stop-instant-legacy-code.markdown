---
layout: post
title: "Stop instant legacy code"
date: 2014-10-08 12:23
comments: true
categories: [development, theory]
---
This might sound strange at first, but there seems to be a habit in development to what it seems encourage the creation of instant legacy code. By that I mean allowing and sometimes encouraging the use of practices that are known to be less
than best by junior developers. While we can't expect people to instantly learn to write extremely high quality code straight off the bat, we can help them not write really low quality code.

# What I mean

Encouraging the writing of low quality code? Sounds crazy doesn't it but I've seen time and again people using the excuse for doing things less than perfect, "It'll be easier for the junior developers to pick up". While I understand where these people are coming from I think it's the exactly the wrong thing we should be doing. At a point where people are learning the most, giving them bad advice isn't going to be helpful in the long run. You may make that one day slightly easier but you've potentially just made their professional life down the line a lot more painful.

# The easy option

As people we normally go for the easy option over the hard option. When you first start out programming a lot of the time you come across two options, one appearing very easy and one appearing very hard. The thing is there really is a disconnect between appearances and reality.

# Example

To explain this better I'll give an example I once came across. I came across a blog post about the correct way to fetch a web resource via https using file_get_contents() in php. When questioned about why he was using it he explained that it would be easier for his junior developers so teaching them how to properly fetch https data is a good idea. Which to be fair knowing the correct way to do it is a good thing. However using file_get_contents() function call to get data via http(s) is not a good thing.


## Why?

One of the main reasons for disliking the use of using file_get_contents() for making http requests is, you're reinventing the wheel. Making HTTP request calls is something that so many people have had to do that there are a bunch of mature, stable, extension libraries out there just to do it. Such as Buzz or Guzzle. Why do something when someone else ahs already done it better.

Secondly with file_get_contents() you're coupling your code to a method of fetching HTTP. If for some reason your code now has to be deployed on a server with a PHP configuration of base open url to false then your code is now going to break and you're going to have to go through and change all your http requests code to a new method.

## It's actually easier the proper way

As I said, someone else has already built HTTP request code which is generally better. You won't have to fix silly bugs, you include it into your code and off your go. So the initial writing part is easier since you're not writing but including it and then reading example code. To me that seems a whole lot simpler.

Then the maintaining it is easier since when you need to change it, you change one line of code in one place. You won't have to look through thousands of lines of code trying to figure out all the places you've made http requests. Going and writing a new method of making HTTP requests. Just change a line. Again seems a whole lot simpler to me.

# Unlearning

Eventually after a while the junior dev isn't going to be so new. They're going to be expected to write high quality code. For them to do that they can't be doing that stuff. One person I seen who was talking about teaching their junior developer something then said in the next sentence that once they had more experience they would teach them (what I consider to be) the proper way of doing it. So some people even know there is going to be a period of unlearning. For me that seems like such a crappy thing to do to someone. Teach them something that at somepoint they are actively going to have to unlearn.

# Teaching the proper way

So instead of teaching developers the proper way to do legacy code, teach them the proper way to do up to date code. This helps you and them.

Now it may seem that if someone asks me a question and I know the answer but the way there are doing is a legacy way I wouldn't answer it. That's not something I would do. If someone asks you how to do something and you know, answer the question then inform them about a better way. Just answering the question and not informing them of the better is just as bad as not answering the question because it's legacy. Both of these aren't helpful to the development of developers. We're not instantly great, we have to work towards it and hope we achieve it. We can only do this if other people help us. Be that other person and stop instant legacy code.
