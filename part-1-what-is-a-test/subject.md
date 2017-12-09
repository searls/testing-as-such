# The Test Subject

If "test" isn't the best term, what would be a better metaphor for this activity
where we carefully design repeatable scenarios that confidently tell us
interesting things about our software?

Actually, that sounds an awful lot like a scientific experiment. That's
right, you've been *doing science* all this time without even realizing it!

In fact, when I began thinking of tests less like vehicle inspections and more
like science experiments, many things that had confused me about testing became
clear. We'll invoke experimentation in several points in later sections, but
first we should discuss a couple foundational ones to get us started.

## The `subject` Name

For starters, something simple: what should we call the thing being tested?

The testing community has gone back and forth on advice about this–trying to
balance expressiveness with consistency—but most programmers settle on naming
the thing-being-tested just as they would in production code. So a test of a
`User` model would assign an instance to `user`. If a test needs to exercise an
interaction between two users, maybe they'd be named `user1` and `user2`.

Unfortunately, if a test becomes long, complicated, or inconsistent, the
question "what's being tested here?" can quickly become unanswerable. (If you're
having trouble imagining such a long, complicated, or inconsistent test that
this could be the case, then you have my deep and resentful envy.)

To mitigate the very real risk of losing track of something so basic as "what
are we even testing", the first step to treating our tests more like experiments
is to consistently call out the thing being tested as our test "subject". This
is why you'll see myself (and hopefully lots of people) use `subject` as the
identifier of first resort in their tests for the thing being tested, like this:

```js
module.exports = function isAdultTest () {
  const subject = new User("Jim", 1956, 11, 17)

  const result = subject.isAdult()

  assert.equal(result, true)
}
```

## The Experimental Mindset

This experimentation meme gives us more to work with than a name to call the
thing being tested, it also helps us reframe questions developers frequently ask
day-to-day about testing. To drive this home, let's look at an example of where
this mindset can be valuable. Suppose your pair partner asks you, **"Should we
fake this function or call the real thing?"**

If you treat tests like you would a midterm exam, then the answer to whether the
modules and integrations your subject interacts with ought to be real or fake is
clear: real is better, because you want your assessment to be as realistic as
possible. Of course, it's impossible to make it _perfectly_ realistic, and it
may be too arduous or time-consuming to make it even _mostly_ realistic, but
there's still likely to be an overriding desire to make each test as realistic
as is _feasible_ given one's time & budget constraints.

The problem with designing tests to run under maximally (feasible) realistic
conditions is that they'll be slow, they'll differ from one another arbitrarily,
and the bar-of-feasibility will change over time and circumstance. Additionally,
they're bad for morale: every instance of a faked HTTP API or replaced method
will feel like some kind of moral concession, and can never be understood as
having been the proper course of action. In all but the simplest cases, this
path leads to slow, hard-to-maintain tests that nobody on the team can explain
clearly. (Fake things that replace real things in tests are called "test
doubles", and are [defined later in this section](test-doubles.html).)

Realism, it turns out, is not an unbounded virtue of good testing practice.

The experiment metaphor, meanwhile, gives us a completely different perspective
by which to approach whether our subject should interact with a real or fake
dependency: that of _experimental control_. If we can draw a clear box around
the test subject to observe whatever we're interested in, then only things that
might influence the subject's behavior based on variable conditions (e.g.
third-party APIs, special days of the week, etc.) should be replaced by fake
things that the test can keep under tight control. With this subtle change of
mindset, anyone on such a team should be able to easily explain and defend why
it was appropriate to fake out, say, a third-party HTTP API throughout a given
set of tests. (This is a weighty topic in its own right, and we'll cover it in
more detail in Part 3's section on [Experimental
Controls](../part-3-how-to-test-well/experimental-controls.html).)
