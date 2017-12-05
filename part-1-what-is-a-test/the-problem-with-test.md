# The Problem with "Test"

Now that we have a working definition of what a test is, let's talk about why
it's perhaps an unfortunate choice of words for our industry to have landed on.
As we'll discuss in [Part II](../part-2-why-write-tests), there's no shortage of
reasons why people write automated tests, but not all of them fit neatly with
other common uses of the English word "test".

Ask yourself: *what comes to mind when you think of the word "test"?*

Odds are, the word "test" evokes images like a 29-point car inspection, in which
a mechanic uses *tools* to  *verify* that *things are working*, especially after
hundreds or thousands of miles of *wear and tear*. If you think harder about the
word, maybe you'll experience flashbacks to *exams* you took in school, which
tried to *score* your *correctness* on a variety of *significant points*. The
next most common association might be to *medical tests*, in which you're
helplessly *poked and prodded* with an expectation that a *diagnosis* will
subsequently *explain some problem* you're experiencing.

The truth is, most programmers were never formally taught about testing, and as
a result bring with them an assortment of preconceived baggage about what the
word "test" should imply about the activity. Reflecting on the emphasized words
and phrases above, it's no surprise that most programmers assume testing is only
about verifying the correctness of software after it's been written.

And they're not wrong, per se. Testing is indeed about verifying the
correctness of already-written software, but that mindset is too narrow to fully
appreciate the broad range of benefits that a thoughtful testing practice can
bring.

Considered more broadly, testing is about generating custom-tailored _feedback_
from software. The simplest and most common feedback we seek via tests is, of
course, that the software is "working" (a separately loaded term for this
usage). But tests can provide other forms of useful feedback, too. Feedback
like:

* Whether the design of the code we're writing makes it easy to set up, invoke,
  and measure its behavior
* The runtime performance of our code, whether benchmarks of isolated critical
  sections or behavior of integrated systems when placed under heavy load
* The degree to which our user interfaces are accessible to everyone
* Whether our code operates at a single level of abstraction, based on things
  like the conditions by which its logic branches or on the uniformity of the
  contracts between our code and its dependencies

The types of feedback we might glean from a test are limited only by the number
of things about our code that we care about. The popular notion that testing is
a simple measure of correctness, meanwhile, oversimplifies testing to the
boolean question, "is it tested?" Until we appreciate the breadth of information
tests can gather for us, teams will continue to value their test suite based on
reductive metrics like [code
coverage](https://en.wikipedia.org/wiki/Code_coverage).

## Speed and Specificity

Why are tests often the right tool to gather so many types of feedback? For two
reasons: tests can be at once very fast and incredibly specific.

Good tests are fast. And feedback, regardless of its purpose, is always more
valuable the earlier and faster it can be provided. Have you ever wondered why
some programmers care so deeply about making their tests and [continuous integration
builds](https://en.wikipedia.org/wiki/Continuous_integration) faster? Or why
developers might spend hours futzing with tools that allow them to rapidly
run only the tests that target the bit of code they're working on? Typically,
it's because they've internalized the lesson that the time it takes to receive
feedback from their software is the chief limiting factor on their
productivity. (We'll discuss the ramifications of this in more detail in Part
3's section on [fast feedback](../part-3-how-to-test-well/fast-feedback).)

Separately, no tool can observe the usability and behavior of a function to as
great a degree of specificity as a test. Isolated unit tests can provide as
narrow and probing a seam by which to test a given function as we can imagine.
Sure, the behavior of any function could probably be observed in a black-box,
integrated way (such as through a browser-based test of a web app), but that
test would be much harder to trace back to the source. When an integrated test
fails, the next step is usually a fact-finding mission to uncover the code that
broke it; any error message we might read will typically be completely divorced
from the function itself. At the opposite end of the spectrum, sufficiently
isolated tests can produce messages that are so localized that they can
literally signal to the developer exactly what to do next, making the practice
of programming feel more like a laid-back game of paint-by-number.  (We'll
discuss the [trade-offs on test
locality](../part-4-where-to-test/locality-vs-decoupling) in Part 4.)

For all these reasons, I'd challenge you to loosen any preconceptions you have
of what a test should be or why someone should or shouldn't write one. As it
turns out, there are a near infinite number of good and bad motivations to write
a test, and the right approach to testing will vary drastically from one
situation to the next.
