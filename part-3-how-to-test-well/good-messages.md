## Assertion messages

One thing to keep in mind is that for folks who write tests in tandem with
production code, assertion design plays a vital role in supporting productivity.
Whatever error messages are produced by the parser, runtime, and assertions
serve as cues, telling the programmer what to do next. In fact, "error" and
"exception" become yet more unfortunate words in this context, because they're
an entirely _expected_ form of continuous feedback when practicing a test-driven
methodology. (We'll talk more about [test-driven
development](../part-5-which-workflow/tdd.md) in Part 5.)

Programmers who aren't in the habit of writing many tests will often recoil at
the sight of error messages, because outside of testing, errors are almost
always unexpected indicators that something went awry. But programmers who write
lots of tests see many _anticipated_ errors in the course of their work, and as
a result are more likely to appreciate good error messages. After all,
the higher the quality of messages the programmer can receive from the system,
the less likely a debugging expedition will be necessary to move past it.

// example of useless asert and what it leads to


// example of normal assert

// example of power-assert

