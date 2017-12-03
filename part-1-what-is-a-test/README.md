# Part I: What is a Test?

It might feel silly going to such great lengths to define something so seemingly
obvious, but before we go any further we're going to take some time to define
what tests are. There is a great deal of confusion surrounding testing
generally, and few things can ward against or dispel confusion as
well as a careful definition.

So, without further ado, here's my definition of a test:

> A test is code that invokes other code and places assertions on its behavior.

This definition is pretty far-reaching, and intentionally so, as automated
testing is, necessarily, nearly as broad and varied as programming itself.

It's worth noting that there are a few things that escape the definition above:

* Any and all manual testing (e.g. [exploratory
  testing](https://en.wikipedia.org/wiki/Exploratory_testing). While important,
  it's sufficiently different to reside outside the scope of most of what we'll
  mean when we refer to a "test"
* Software that verifies _itself_, particularly at runtime. While similar in
  purpose to a test, runtime assertions tend to have more in common with
  exception handling and guard clauses than test design
* Test files that invoke something but don't assert anything. These are just
  a convoluted way to execute a program to see that it doesn't blow up,
  potentially contributing to [code
  coverage](https://en.wikipedia.org/wiki/Code_coverage) statistics in the
  process

In the same vein, a number of things could fall under this definition of test
that may not typically come to mind. Using a REPL to ensure that a function
behaves as we expect it to could be considered a test, even if the session is
never persisted to disk. Likewise, a scratch file of assertions that one might
keep to use to bolster their confidence as they work is still a test, even if
it's never committed to version control.

## Our first test

Given this very broad and amorphous definition, let's try our hand at writing a
simple test.

Let's start with a simple module to place under test:

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
it's hardly a robust test of the function it's testing, but it will raise an
alarm if the `add()` function fails to meet its expectation.

We can run the test with the `node` binary:

```
$ node add.test.js
```

Nothing is output, which isn't very reassuring, but since the command exits
cleanly, it's probably safe to infer that should means "it's working". It may
not be full-featured by modern standards, but there's no doubt that
`add.test.js` is testing `add.js`.

Note that nowhere in this example did we run a test runner from the command
line, install an assertions library, or use any other tool but our runtime.
These things are ubiquitous and helpful aids for authoring and maintaining
tests, but don't ever let anyone tell you they're inherently necessary to test
your software. This is a point worth emphasizing: you alone are in control of
how you get feedback from your system that the code you're writing is

