Good Afternoon everyone, my last two projects for innovation Fridays were
failures so instead I read a book. (I was going to add Kafka as event handler
to lymph). And today I am going to talk about that book, more specifically
about the boundaries that people should keep in mind while adopting service
oriented architecture.

So I am going to begin with a story. How many of you here have heard or read
about "The Stevey's platform rant".
This guy called Steve Yegge was a developer at Amazon before he moved to Google
and after spending some time at Google he wrote this rant for sharing it
privately, but somehow it became public. It highlights really interesting
differences about how Google does things and how Amazon does things. A thing
that this rant revealed was the infamous email by Jeff Bezos to the tech
department stating that 

"All teams will henceforth expose their data and functionality through service
interfaces"

It had 5 other points; ending with "Anyone who doesn't do this will be fired" 
Bezos is a well known micro manager, well Steve Jobs with fashion or design
sense. 

(Anyways) That email was sent around 2005, 10 years ago, and today Amazon has
embraced this way of development and is one of the biggest platforms built over
services.

They obviously had a lot of learnings and made a lot of discoveries made during
this tranformation.

The service interface must hold their contract, it is the holy grail.
Versioning becomes really important.

Every service becomes a potential for DDOS attack from services with the
network; services should instill throttling or caps.

Services will get lost - there should be a standard way of deploying and
discovering your services

You need a lot of monitoring, you need to keep track of number of requests that
come into your services, the response time, the origin and abnormalities should
raise an alarm. Every team should monitor the services they own.

If you haven't read this rant, I suggest you go online and read it. It would be
worth your time. This and the article by Martin Fowler was my first exposure
to the learnings of service architecture. 

And the book, "Building Microservices" goes into details about these learnings
and more.

One of the things this book talks about is "Boundaries", but before I talk
about what boundaries here is the slide that shows the benefits or using a
service oriented architecture. Obviously this way of developing things is not a
silver bullet, but if done right it promises a lot. It promises agility, speed
of development, self paced teams, freedom, innovation and so on. But sometimes
the promises feel like empty, fall apart.

The two words that stand out for me are freedom and innovation. Everyone likes
freedom, freedom to express themselves be it in how they write code, even the
language they want to use, how they design interfaces, what technologies they
use - the decision to use relational database or a non relational database. How
they write their documentation. How they deploy their services. I believe these
are exploited when teams starts developing services and eventually leads to a
bad services design.

I believe when you start moving towards a services based architecture, you need
to define solid standards. You should define some kind of coding standard, if a
developer moves from one team to another he shouldn't have to change his coding
style, he should be able to figure out where to find stuff. Design standard,
when you start developing a service there should be a standard way you write
the spec, a standard way to name the interfaces, what the return format should
look like, how errors should look like.

Probably the most controversial ones, is the technology standard. We have a set
of technoligies that we work with everyday. I am going to go ahead and call the
set of technologies "SPACE".

Lets see what we have in our DHH "SPACE"

 - We have our servers, lab machines, basically hardware
 - We have our provisioning services - running over mesos with marathon
 - We have our scheduling services - running over mesos with chronos
 - We have our configuration management - (environments, ZK)
 - We have our discovery - (ZK)
 - We have our caching - (Memcache, Varnish, Redis)
 - We have our CI - Jenkins
 - We have our data storage - (postges, ES, Redis)
 - We have our event system - (RabbitMQ)

Rules around the "SPACE"

 - Pick from stuff from the space
 - Write a spec pertaining to a design standard
 - Code should be covered by tests/CI
 - use service discovery to discover services
 - communicate via network (RPC/HTTP?)
 - emit appropriate events
 - monitor all the things
 - as idempontent as possible
 - ....

A lot of these things come for free when you use lymph :)

A simple use case would be, lets say a team wants to develop a service that
suggests restaurants based on which restaurants you have ordered from before.
This looks like a really good use case for a graph database. You can have
relations between restaurants, degrees or seperations, could be potentially
really fast. But if you look at hour space, we don't have graph database. I
believe the team should go back to the drawing board and develop the service
using something that we have in our space. Maybe, the percolate functionality
of Elasticsearch could deliver similar results.

Basically, these space and rules around space is what the book calls
boundaries. It gives examples of what twitter and netflixes boundaries look
like, but quite implicitly. 

So in conclusion, if we go ahead and define our boundaries and follow them we
would be able to get most out of the services architecture that we are
adopting.
