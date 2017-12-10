# Assertions

One thing we can't leave out (lest our [definition](README.md) prove
circular) is a few words on what assertions are and the role they play in
testing.

An assertion is any bit of code that measures something about the behavior or
state of whatever is being executed and can raise some kind of red flag to the
test author when their expectations aren't being met.

Assertions can vary wildly in how sophisticated they are, and anything beyond
trivial spot-checks typically need to be rolled into a library or utility to
avoid muddying the intention of the test itself. Even still, some assertion
libraries are overwhelmingly simple and some are among the most complex
open source projects in a given ecosystem.

How do they differ and why haven't we settled on a clear winning assertion
strategy? Because each approach to writing an assertion provides different
benefits and drawbacks. To illustrate, an assertion might:

* Do nothing more than throw an error message. `if (result !== 5) { throw …` is
  a perfectly valid assertion. Its behavior is obvious, but it wouldn't provide
  a very useful message to the console (e.g. what the value of `result` actually
  was) if it failed. Additionally, explicit logical branching in tests would
  likely confuse the story the test is trying to tell
* Use a bare-bones assertion library like the Node.js [assert
  module](https://nodejs.org/api/assert.html), which provides basic methods like
  `assert()`, `assert.equal()`, and `assert.deepEqual()`. Its messages are
  basic, but the abstraction is so straightforward that the reader could
  probably intuit the implementation of any of its methods without having to
  refer to its source
* Use a sophisticated assertion library like [Chai](http://chaijs.com), which
  provides everything from several API dialects, cute property chaining (e.g.
  `expect(api).to.be(fancy)`. Users of libraries like these often do so in order
  that their tests might clearly _express the intent_ of their code, but usually
  at the cost of comprehensibility to people who lack deep familiarity with the
  library's behavior, which can sometimes make their use contentious
* Use an advanced assertion decorator like
  [power-assert](https://github.com/power-assert-js/power-assert) that takes a
  simple assertion API and then runs each invocation through a full parser so it
  can—in the event of a failure—print lots of information about the actual and
  expected values

An additional wrinkle about assertions is in how they indicate a failure
occurred. Standalone assertion libraries will often throw an error, immediately
halting the current test. In turn, nearly all test runners interpret an uncaught
exception as a failing test and print the message.

However, sometimes the assertion library is integrated with the test runner in
such a way as to run all of the assertions without throwing an error, but rather
registering any failures with the test runner. In cases like this, test output
can often show not just the count of tests, but the number of assertions that
passed, failed, or were skipped. Along similar lines, an assertion library that
is coupled to a test runner can sometimes facilitate advanced features like
pending tests (tests of thought-to-be unfinished features which fail only when
all assertions pass).

None of these approaches are any more "right" than any other, and which is
appropriate will vary from context to context. What's important to understand
for now is that an assertion is a bit of code that indicates a test failure and
produces a message to help the programmer understand what went wrong and what to
do next. (The messages produced by a test's assertions turn out to be vital to
the maintainability of a test suite, and we'll discuss more about [assertion
messages](part-3-how-to-test-well/good-messages.md) in Part 3.)
