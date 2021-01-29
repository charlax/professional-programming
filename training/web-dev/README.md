<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Learning web development](#learning-web-development)
  - [Goal of this training](#goal-of-this-training)
  - [Prerequisites](#prerequisites)
  - [Principles](#principles)
  - [Roadmap](#roadmap)
  - [Meta: learning about learning](#meta-learning-about-learning)
  - [Topics](#topics)
    - [Pick a powerful text editor and learn its ins and outs](#pick-a-powerful-text-editor-and-learn-its-ins-and-outs)
    - [Learn the ins and outs of a programming language](#learn-the-ins-and-outs-of-a-programming-language)
    - [Learn the topics of web development](#learn-the-topics-of-web-development)
      - [Architecture](#architecture)
      - [Best practices, attitude](#best-practices-attitude)
      - [DB and SQL](#db-and-sql)
      - [Dev environment, command line and Linux](#dev-environment-command-line-and-linux)
      - [Distributed systems](#distributed-systems)
      - [Network, protocols, HTTP](#network-protocols-http)
      - [Project management](#project-management)
      - [Security](#security)
      - [Version control (git)](#version-control-git)
  - [Other lists](#other-lists)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

<!--TOC-->

# Learning web development

## Goal of this training

This training provides an opinionated ramp-up program for web developers.

## Prerequisites

Not much, just general knowledge about computer and the Internet.

## Principles

- Focus on the main stuff. A lot of things have to be learnt on the job anyway.
- For aspiring professionals. Programming is not only about raw knowledge,
  it's also about best practices.
- Go wide.
- We learn by doing, so this training includes lots of exercises.
- A lot of videos are included, since they provide hands-on experiences.

## Roadmap

1. Start with a programming language.
2. Do a first pass at the web development components: DB, HTTP API, etc.
3. Write a full-fledged exercise, get it reviewed.
4. Go deeper in the topics above.

## Meta: learning about learning

Feel free to checkout some of the articles about [Learning and memorizing](https://github.com/charlax/professional-programming#learning--memorizing)

## Topics

### Pick a powerful text editor and learn its ins and outs

VSCode is a strong pick nowadays (I use and obviously prefer Vim :).

Make sure to spend a lot of time in your text editor, watch tutorials about
advanced features, install extensions, learn all the main keyboard shortcuts,
subscribe to mailing lists about it, etc.

You will spend most of your time within your text editor. Turn it into your
ally!

### Learn the ins and outs of a programming language

A developer's main tool being the programming language, it is important to
achieve high proficiency in at least one of them.

I'd recommend starting with Python or TypeScript.

For Python, you can have a look at my repo [charlax/python-education](https://github.com/charlax/python-education).

To ensure you have good command of the language, you should try out some of
those exercises:

- [Exercism](https://exercism.io/) (get free code reviews!)
- [Small Python exercises](https://github.com/charlax/python-education/tree/master/learning-python/exercises)
- [danistefanovic/build-your-own-x](https://github.com/danistefanovic/build-your-own-x) (for instance: build a [git in Python](https://wyag.thb.lt/))
- [Other list of exercises](https://github.com/charlax/python-education#exercises)

Learn how to handle:

- Regexes
    - Do exercises
- Functional programming
    - [Functional Programming Fundamentals](https://www.matthewgerstman.com/tech/functional-programming-fundamentals/)
- Design in patterns
    - E.g. [in Python](https://medium.com/@daniel.heller/ten-principles-for-growth-69015e08c35b))
- Tests
    - [Why bother writing tests at all?](https://dave.cheney.net/2019/05/14/why-bother-writing-tests-at-all)
- Crazy things in languages
    - 🎞 [Wat](https://www.destroyallsoftware.com/talks/wat)

If you have time, learn more programming languages, starting with some that are
*very* different from your main one:

- Haskell
- Clojure
- Kotlin
- Rust
- Assembly

### Learn the topics of web development

Note: this is just a short selection of stuff listed in
[charlax/professional-programming](https://github.com/charlax/professional-programming).

Start your career the right way with this article: [Ten Principles for Growth as an Engineer](https://medium.com/@daniel.heller/ten-principles-for-growth-69015e08c35b)

#### Architecture

- Learn about DDD (domain driven design)
- Wander in the [Software Architecture Guide](https://martinfowler.com/architecture/)
- 🎞 [On the Spectrum of Abstraction](https://www.youtube.com/watch?v=mVVNJKv9esE&ab_channel=ReactEurope)
- 🎞 [Simple Made Easy](https://www.infoq.com/presentations/Simple-Made-Easy/)

#### Best practices, attitude

Read one of those:

- 📖 [The Pragmatic Programmer: From Journeyman to
  Master](https://pragprog.com/titles/tpp20/): hands-on the most inspiring and useful book I've read about programming.
- 📖 [Code Complete: A Practical Handbook of Software
  Construction](http://www.amazon.com/Code-Complete-Practical-Handbook-Construction/dp/0735619670): a nice addition to The Pragmatic Programmer, gives you the necessary framework to talk about code.

Read of the resources listed under [Must-read articles](https://github.com/charlax/professional-programming#must-read-articles).

#### DB and SQL

- Learn basic and advanced SQL: joins, indexes, subqueries
- Install Postgres and play with it.
- [Do those postgres exercises](https://pgexercises.com/)
- Learn about ORM
    - 🎞 [Watch this Python introduction to ORMs](https://www.youtube.com/watch?v=P141KRbxVKc&ab_channel=PyCon2014) (with SQLAlchemy)

#### Dev environment, command line and Linux

- [jlevy/the-art-of-command-line](https://github.com/jlevy/the-art-of-command-line): master the command line, in one page
- [Linux Productivity Tools](https://www.usenix.org/sites/default/files/conference/protected-files/lisa19_maheshwari.pdf)
- Do shell exercises
- Install/use some of those tools: https://github.com/jondot/awesome-devenv
- Write your own dotfiles: https://github.com/webpro/awesome-dotfiles (you
  checkout mines: https://github.com/charlax/dotfiles)
- Learn about Docker
    - 🎞 [Containers From Scratch](https://www.youtube.com/watch?v=8fi7uSYlOdc&ab_channel=GOTOConferences)

#### Distributed systems

- DDIA
- [The Log: What every software engineer should know about real-time data's unifying abstraction](https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying)
- [donnemartin/system-design-primer](https://github.com/donnemartin/system-design-primer): learn how to design large-scale systems.

#### Network, protocols, HTTP

- [How Does the Internet Work?](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)
- [vasanthk/how-web-works](https://github.com/vasanthk/how-web-works): what happens behind the scenes when we type www.google.com in a browser?
- Learn about the basics of TCP and UDP
- Learn the basics of the HTTP protocol: header, verb, status code, TLS, etc.

#### Project management

- [Efficient Software Project Management at its Roots](https://blog.pragmaticengineer.com/efficient-software-project-management-at-its-roots/)
- [How to Lead a Project - as a Software Engineer](https://blog.pragmaticengineer.com/how-to-lead-a-project-in-software-development/)
- [TechnicalDebt](https://martinfowler.com/bliki/TechnicalDebt.html)

Checkout this section on [charlax/engineering-management](https://github.com/charlax/engineering-management#project-management)

#### Security

- Learn about the OWASP Top 10

#### Version control (git)


## Other lists

- [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/) (MIT).
- [What every computer science major should know](http://matt.might.net/articles/what-cs-majors-should-know/)
- [Teach Yourself Computer Science](https://teachyourselfcs.com/)
