In development we constantly bemoan bad developers. But what I've noticed is everyone generally thinks they're going a good job and the other developers are bad. I don't think you can exactly define what is a good developer down to a tea but I think you can have rough benchmarks signs of if you're good or not. These are generally if you follow well defined practices. They're are levels of development practices ranging from the basics (DRY) to advance (CQRS).

It's my opinion that you're only as good as the level of practices you follow well. So if you only do intermediate practices you're an intermediate developer. If you do intermediate practices well but mildy-advance practices poorly you're still an intermediate developer.

I think it's important to say that my definition of well is applying them in the majority of cases. No one is perfect so we obviously make mistakes and write poor code from time to time for various reasons. Also it's important this isn't a 100% guide as there are most likely hundreds of things I'm not thinking of. I'm also an OO PHP developer so a lot these may be related to OO. However I suspect majority of them can also be applied to other programming paradigms.

I'm also not saying I do all of these things. I'm just aware they exist and I rank them at a certain level. Some times I don't even think I have a full grasp of the concept. Nor am I making any claims that I'm any good. Like everyone I am still learning and trying to be a good developer. I think understanding our flaws helps with this.

# Basics

The fundamentals every programmer should have.

## DRY - Don't repeat yourself

I consider this programming 101. It's a fundamental practice which nearly all good development practices are based on. It's very simple the aim is never repeat yourself. Easiest time to know if you're breaching this is if you literally copy and past code from one function to another.

However sometimes the repetition can be more subtle and you end up having transform data from one format to another repeatedly throughout your system. Like the example below. Every time you want to use the data from getData you have to call unserialize.

```php
$data = unserialize(getData());
```

For more info see

## Encapsulation

Encapsulation is when you round up stuff that are related and put them together. I feel this is very important thing to do.

On a simple case, say you want to do create an invoice. You wouldn't want to have use an object to add items to the invoice and then you use a different object to get the total for the invoice. You would want to use one object to add lines and when you added the lines and then use the same object to get the total value of the invoice.

Another example is the the example of breaching DRY. The data was stored in a specific format however as far as the rest of the system is concerned it needs to be another format. Therefore you should encapsulate the logic of how it's stored to the storage layer.

Encapsulation doesn't mean it's all in one class. But in the same place, be that module, class, namespace. For example you wouldn't want to be doing Delivery logic in your Invoice module.

The benefits are very simple if you want to know how something works you just look in one place. If you want to change how something works you just make the change in one place.

For more info see


## Round up
TODO move to bottom
In my opinion these are are things you must do as a developer. Not doing them efficiently means you are a bad developer. Even as a junior developer you should still be doing these things reasonably well after 6 months or so experience.

This is not if you do them all the time, but do them consistently.

# Intermediate

TODO

## Single responsibility

The basics of Single responsibility it each object so only be responisble for one thing.

For example you should never have a class that is respo nsible for inserting data in to the database and for making HTTP requests to AWS to create new server instances. So you would have a class that would do the insertion into the database and then another class to create new AWS instances.

A quick guide to know if you're breaching Single responsibility, you ask yourself what does this class do and if you use the word "and" you're probably breaching single responsibility.

For more info see

## Open/close principal

The open/close principal means your class is open to extension but closed to modification. The basics of it is I should be able to extend a class to add extra functionality. I however should not be able to change how it works.

For example an Order entity class. I should be able to extend it so I can describe specific kinds of Orders such as PrePaidOrder and CreditOrder. But I should not be able to change it to say remove a field within the order entity.

Another example I should be able to extend a sorting class so it can sort other kinds of things but I shouldn't be able to change it from a sorting class to first item found class.

For more info see

## Liskov's object replacement

The object replacement principal is that I should be able to replace any object with one of the same type and not change the behavior of the application.

For example if I change the database class for another the application should not go from saving data about servers to managing the AWS instances.

For more info see

## Interface segeration

Interface segaration is simply just Single responsibility but for interfaces. The basics of it is no object should be forced to implement a method that it doesn't need.

For example a translator class can imp

For more info see

## Dependency Inversion

Not to be confused with Dependency injection, which Dependency Inversion helps with.

Dependency Inversion is when you make your class coupled to an abstract/compsite instead of the concrete version. So your class never knows about the existance of the actual implement that it'll use. While the implementation class never knows about the existence of anything that uses it.

This makes Dependency injecting and object replacement really simple.

For more info see

## Automated Testing

This is where you use write unit/integration/system tests so you can test you entire code easily.

It's important to note this isn't just doing TDD, but any testing. While I fully believe that TDD is the best way to test and write code. I don't believe it's the only way or that by writing tests after you wrote the code makes you any less of a developer.

If you don't have tests and you change something, how can you be sure it works? Simply you don't. Even when you don't have tests you still test your code, you just do it by hand. Which isn't as anywhere near efficient as having it done by code.

For more info see

## Correct tool for correct job

This isn't exactly an official practice per say. But it seems like such an obvious thing. Using the correct tool for the correct job seems obivous but as people who often break this, how often have you used something other than a bottle opener to open a bottle of beer. This is not just a software developer problem, but I believe to be a really good developer then consistently you will use the correct tool for the correct job.

Some examples of not using the correct tool for the correct job. Putting functions code in a class then just calling those method procedurally. Using automated testing tools to mointor your production web application. Using static code analysisers to run your CI. Using MongoDB to store relational and transactional data.

## Round up

While before with the basics it was all or nothing. I think with this level of stuff you have various levels of proficiently depending on how many you actually do.

# Advance

At this level a lot of these things seem to go hand in hand in my opinion.

## Law of demeter

This is very simple your code only ever talks to/uses objects it knows exists directly.

For example if you inject a query object into a method that method should then never access the query object to get to a parameter bag object. Instead what you do is create a method on the query object that calls the parameter bag object and returns the data you want. The benefits of this means you can refactor eaiser since you can clearly see where code is used and where it isn't. So if you were to change how the parameter bag works you only have to change it in the query class and not in every place the query class is used to pass the parameter bag.

For more info see

## CQRS - Command query responsibility segeration

Command query read segeration is a principal at the heart of is about seperating your reads from your writes. In my opinion you can apply this on several levels. For almost everything I think a on method level applys. But there is also on class level. And then there is system/service level which is actually the proper CQRS.

On the method level no method that does a read should also be doing a write. But on an class level you no class that does reads should be doing writes.

But for the proper definition of CQRS, a command is something that does a write. A query is something that does a read. When doing commands to the system you should use a different pathway/service than if you were just querying it.

For more info see

## Domain modeling

In simplist form this is seperating the Domain/business logic away from the rest of the code and understanding what is part of the domain and what is actual implementation.

## Domain Driven Design

This is a rather complex topic and this little section will not give it any justice.

Doing DDD involes a lot more than just domain modelling. It means commicating with the business team to find the correct model for the domain and applying it. In my opinion the key to DDD is ubiqutous language. In which you use the same terminogly as the the business people and then use that terminogly in the code.

For more info see

## Hexagonal Architecture

Hexagonal Architecture is simply isolating your domain model from your application layer and seperating your application layer from third party items.

So you have your domain model. Which should remain seperate from everything and coupled to nothing. Next you have your application layer which is coupled to your domain model. At which point you have your outlayer which uses the application layer and third party items. Such as databases and APIs.

This allows you to change third party items without having to worry about your domain model or your how your application works.

For more info see

## BDD

Behavior driven development is in it's simplist form talking with the business team in a language they understand to workout what actually needs built.

This again can get really complex and there are many different ways of doing BDD and many different practices.

For more info see

## YAGNI - You aren't gonna need it

YAGNI comes originally from Xtreme Programming and it's a concept of don't build something until you need it. As developers we look at our road map and see that in 6 months we'll be building some feature that is semi related to what we're currently working on. So we decide to implement the stuff that feature will need now while we're in that area anyway. However the thing is roadmaps generally change and in 6 months that feature you have half implemented is no longer required and now you're left with a bunch of useless code floating around your system.

This while it seems like a simple concept I think this is more about realising that YAGNI which I think can be quite hard to do at times.

For more info see

## Teir Architecture

Teir Architecture is simply splitting out the responsibility of system responsibility on different layers of systems. So you start off with a web system layer which has no access to the database. Any time it needs to fetch something from the database it then makes a request to the database level which has the ability to do reads. Any time it needs to do a write it then makes a request to the write layer which then does writes.

For more info see

## Service Orienated Architecture

This is when you build applications to handle specific jobs. Each service only knows about what it needs to do and is decoupled from other services.

So for example if your application needs to send communication you could have a communication service that all it did was send communications. It didn't know about any of the logic about why the communication needs to be sent just that it needs to be send and does the sending.

For more info see


## Correct terminogly

While this may sound a bit snobby we generally have a habit of using the wrong terminolgy when talking about thinks. While you may think what does it matter what it's called? Well it doesn't but it does matter if you're able to correctly define to others what you're doing or thinking about doing. For example if you say blackbox testing sucks when what you mean is System level testing sucks, it can lead to people like me pointing out that block box testing is very efficent way of testing.

One way I think of it is, if you don't know what you're doing what are you doing?

# Not included

I also think it should be noted things that are not listed here and to understand why I haven't listed them. Personally I think you should probably do them all but I don't think they necessary make you a better developer.

## Programming outside of work hours

A lot of people seem to think to be a good developer you must spend all your time Programming. I personally don't think this is the case. One of the reasons is I think your brain needs time to rest. Also spending all your free time playing music doesn't affect the quality of work you do during office hours.

## Contributing to open source

While contributing to open source is great and will most likely help your fundamental software development skills. In my opinion it will also teach you some bad such as not fixing bugs because they've existed for so long people expect it to work like that. While I think that's the correct thing to do with an open source project which other people rely on. Not fixing bugs in a private company because some people may expect it to work the broken way isn't really good. I think all bugs should be fixed.

## Programming in more than one language

While I think it's a good idea to play with other programming languages and you will improve your development skills. I don't think being able to code in C and Perl will make you a better PHP developer. Just because you know how to do terrible things in multiple languages doesn't make you a better developer than one who knows how to do good things in only one language.

## Use of specific tools

For example I am not going to say to be a good developer you have to use Jenkins, a fully featured IDE, a good debugger tool, etc. While I would say you should use them, not using them doesn't affect your ability to write high quality code. I just think they'll make your life easier.

## Design patterns

Design patterns are most certainly part of writing good clean high quality code. However I feel to often people ask "Do you use design patterns?". Well the answer to that is generally always yes. Knowing the code you write is a design pattern doesn't make you good. What makes you good is that you automatically wrote good code.

I also think people try to jam design patterns into problems than solving the problem the design pattern solves. We seem to obsessed with design patterns.

I also don't think your code is any less of if you solve a problem that has a design pattern with another method that is also clean and follows good development guidelines.

## Pair Programming

I know some people who assume if you don't pair program you're not as good as the people who do. Some people just don't like pair programming (myself included). While I think pair programming is smart and extremely useful in many situations I don't think it should be defined as the only way to go in those situations.

## Code Kata

While I think doing code katas is a lot of fun and a wise move. I just don't think that not doing it removes you understanding and ability to implement any of the best practices in development. I think it'll help you learn and improve those abilities.

## Continous Integration

Many people think Continous integration is simply running all your tests after each commit. Or even just using Jenkins before you merge so "master" is deployable. However Continous integration is a practice of everyone working on the same branch and all commiting to the same branch. So everyones work is integrated continously. With the minmum of if you're using branches that it's merged into master at the end of the day. This in my opinion makes this a team discipline and not a single developers discipline.

## Agile

Agile in it's many forms it a method of managing the project. You can be a good developer producing good work without doing Agile.

# Round up
