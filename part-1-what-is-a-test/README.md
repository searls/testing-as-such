# Part I: What is a Test?

It might feel silly defining something so seemingly obvious, but before we go
any further we're going to take some time to choose a definition for what tests
are and are not for the purpose of this guide. There is a great deal of
confusion surrounding testing generally, and few things can ward against or
dispel confusion as effectively as a careful definition.

So, without further ado, here's our definition of a test:

> A test is code that invokes other code and places assertions on its behavior.

It's necessary that our definition be pretty far-reaching, as testing can be
nearly as broad and varied as programming itself.

It's worth noting that there are a few things that escape the definition above:

* Any and all manual testing (e.g. [exploratory
  testing](https://en.wikipedia.org/wiki/Exploratory_testing)). While good
  manual testing is very important, it's different enough that most of what we
  say about "testing" won't rightly apply to it
* Software that verifies _itself_, particularly at runtime. While similar in
  purpose to a test, runtime assertions tend to have more in common with
  exception handling and guard clauses than with test design as most people
  understand it
* Test files that invoke something but don't assert anything. These are just a
  convoluted way to execute a program to see that it doesn't blow up (regardless
  of whether they contribute to [code
  coverage](https://en.wikipedia.org/wiki/Code_coverage) statistics in the
  process)

In the same vein, a number of things could fall under this definition of test
that may not typically come to mind. Using a REPL to ensure that a function
behaves as we expect could be considered a test, even if the session is never
persisted to disk. Likewise, a scratch file of assertions that one might keep at
their side in order to bolster their confidence as they work still qualifies as
a test, even if it's never committed to version control.

Note also that nothing about this definition constrains one's motivation in
writing tests; while most tests are written to ensure a bit of code is working,
it's no less valid for a test to exist primarily to give the author feedback on
the usability of an object's design.

## Our first test

Given this very broad and amorphous definition, let's try our hand at writing a
simple test. Let's start with a simple module:

```js
// add.js
module.exports = function add (a, b) {
  return a + b
}
```

A test of this `add` module could be as simple as this:

```js
// add.test.js
if (require('./add')(1,2) !== 3) {
  throw new Error('add() is broken')
}
```

The file `add.test.js` qualifies as a test, because it invokes the `add` module
and asserts something about its behavior. It only covers a single example, so
it's hardly a robust test of the function, but it will raise an
alarm if the `add()` function fails to meet its expectation.

We can run the test with the `node` binary:

```
$ node add.test.js
```

Nothing is output, which isn't especially reassuring, but since the command
exits cleanly, it's probably safe to infer that means it's working. It
may not be full-featured by modern standards, but there's no doubt that
`add.test.js` is indeed a test of `add.js`.

Note that nowhere in this example did we call a test runner from the command
line, install an assertion library, or use any other tool but our runtime.
These things are ubiquitous and helpful aids for authoring and maintaining
tests, but never let anyone tell you they're inherently necessary to test
your software.

This is a point worth emphasizing: you are in near-total control of how you get
feedback on the code you write. If one-off test scripts like the one above are
too cumbersome, then you might adopt tools to eliminate drudgery.
If running your tests is too slow to enable the productivity of rapid feedback
loops, you might find yourself stripping out some of the complexity and
indirection that testing tools often introduce.  Choosing the right tools for
the situation at hand and then employing them to the right extent is just the
first of many tradeoffs to be negotiated with respect to testing.
