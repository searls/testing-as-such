# Testing as Such

## Introduction

Welcome! This is a little book about testing. I've been thinking way too hard
about automated testing for over a decade now, and want to put down some of the
more useful conclusions I've arrived at for the benefit of other software
developers.

Nearly everything I'll write in this book is a curated remix of things I learned
from [Kent
Beck](https://www.amazon.com/Extreme-Programming-Explained-Embrace-Change/dp/0321278658),
[Gerard
Meszaros](https://www.amazon.com/xUnit-Test-Patterns-Refactoring-Code/dp/0131495054/ref=sr_1_1?s=books&ie=UTF8&qid=1512288184&sr=1-1&keywords=xunit+patterns),
[Michael
Feathers](https://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052/ref=sr_1_1?s=books&ie=UTF8&qid=1512288214&sr=1-1&keywords=working+effectively+with+legacy+code),
[Steve Freeman & Nat
Pryce](https://www.amazon.com/Growing-Object-Oriented-Software-Guided-Tests/dp/0321503627/ref=sr_1_1?s=books&ie=UTF8&qid=1512288237&sr=1-1&keywords=growing+object-oriented+software%2C+guided+by+tests),
[Jim
Weirich](https://www.wired.com/story/giving-open-source-projects-life-after-a-developers-death/),
my colleagues at [Test Double](https://testdouble.com/agency), and surely
countless others. Keen observers will surely notice numerous inspirations from
various communities that have contributed to testing over the years.

While much of the wisdom of those who came before me still stands on its own,
software is a fast-moving and fickle industry. We often struggle to appreciate
advice that isn't packaged in the dominant programming languages and tools of
the day.  But it's not enough to reapply a sheen of novelty on old ideas.
Learning how to test well is hard enough as it is, and it would be unfair
to ask someone to translate examples created for a programming language they
don't know, or to tease out timeless wisdom from transient advice that was
coupled to the context of a bygone era.

As a result, this book is a retelling of those stories (alongside a few new
ones), and is unavoidably wrapped up in the context of someone writing a lot of
JavaScript at the tail end of 2017. I hope some of it withstands the test of
time, but I won't mind if it doesn't—so long as it helps even a few of my
contemporaries succeed with testing.

## Who this book is for

While most of the things things I'll write here will apply to most languages and
contexts, it's being written with the JavaScript application developer in mind.
When I began exhorting developers to test their JavaScript in 2010, it was an
uphill battle; in part, because few programmers identified as "JavaScript
developers".  Now, a mere seven years later, and it feels like JavaScript has
eaten the world. The message that testing one's code is a good idea no longer
needs to be sold. If anything, we now have the opposite problem: the universe of
people writing JavaScript is so massive and diffuse that it's rare to find a
consistent, coherent voice on testing. Worse still, the constant churn of
popular testing tools has deferred any thoughtful conversation about testing as
a practice.

This book is for people who want to learn to write good tests in a way that will
live beyond the popular testing tools and application frameworks of the day.
When the Next Big Thing™ comes along, most of this advice will continue to serve
you well. The half-life of JavaScript tools is simply too short to continue to
couple one's philosophy on testing & design to any one library.

So, who is this book especially written in mind for? Well:

* If you're new to testing, this book is for you
* If you're not new to testing, but you're to some degree disillusioned with it,
  then this book is for you
* If you find your application code is hard to change and maintain over a long
  lifespan and you're open to the premise that good testing can encourage usable
  code design, then this book is for you

## Approach

I won't lie: testing is a massive topic and we have a lot of ground to cover.

We'll start by laying the foundation: defining what a test is and giving names
to several of the qualities that characterize most automated tests. Next, we'll
discuss various motivations that developers and teams typically have for writing
tests. We'll then move on to unabashed advice on what separates good tests from
bad. With that in place, we'll piece together broader strategies for planning
suites of tests to support entire applications and complex sysstems. Finally,
we'll end with several of the testing workflows that can guide how you write
production code, along with sufficient instruction on how to try your hand at
them.



