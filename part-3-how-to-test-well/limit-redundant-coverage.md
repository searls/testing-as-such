# Limit Redundant Coverage

Let's talk about "redundant code coverage", and why it's—perhaps
counter-intuitively—a bad thing.

Many testing advocates like to use the expression, "measure twice, cut once" to
describe testing's desired benefit of providing steady forward progress, even at
the expense of (short-term) speed. It's a rare case of a popular idiom that
actually rings true when applied to software.

But many of those same advocates will go on to write:

1. Tests through the browser
2. Tests of the HTTP router the browser visits
3. Tests of the controller the router delegates to
4. Tests of the repository the controller queries
5. Tests of the model the repository fetches

(Where each of those tests calling through to the layers beneath them, including
whatever data store the app relies on.)

That means a change to a bit of behavior in a model object could easily violate
assertions in the many layers of tests above. If a controller test asserts that
adding a set of invoices will yield a total of `$31.44`, it's unlikely anyone
would have realized the assertion was incidentally depending on, say, detailed
taxation rules deep inside the `LineItem` model.  Therefore, when a tax rule
changes, the intended-to-be-unrelated controller test will also fail, sending
someone on a fact-finding mission to divine whether the controller logic is
broken or the assertion simply needs to be updated.

It gets worse. Applications tend to have many more pages & components than they
have distinct model types, which means that a single change to a model might
break dozens or hundreds of other tests. I'll never forget the time when my
colleague James was tasked with a trivial change to how our application rounded
financial transactions. The change itself took him thirty minutes, but it took a
group of three of us two weeks to get the build passing after the "minor" change
subtly broke thousands of tests.

There's a reason the saying is *measure twice, cut once*. Perhaps *measure two
thousand times, cut once* just didn't have the same ring to it.

You may see now why "redundant code coverage" is not a quality to be celebrated.
On its face, one might infer from the term that the system is being tested
rigorously and from every perceivable angle. And while it's true that there's a
chance that yet-another-test might find a defect that no previous test could,
the odds are usually remote.

The absolutist mindset that demands tests catch _every possible bug_ without
regard for cost  is depressingly common, and almost always leads to ruin. The
story plays out the same way nearly every time:

1. A team adopts testing with dreams that it will be a panacea from whatever
   ails them (e.g. lack of confidence in making changes, lots of production
   defects)
2. The team writes so many tests that many frequently-changed functions might be
   invoked tens of thousands of times over the course of the build
3. Gradually, the pace at which the team can change the system slows down again.
   Not because it takes longer to confidently change the code, but because each
   code change yields many times more changes to their tests
4. The team realizes their once-liberating test suite is now an albatross, but
   they have little recourse. The tests are their source of confidence, and no
   one feels they have the authority to start deleting them
5. There is no step five

The slowly-constricting vice grip that redundant code coverage represents is so
difficult to escape that most popular advice is limited to preventative
measures.  That said, there are some ways to loosen a test suite's grip on a
team's productivity.

## Preventing redundant coverage

Developers who have been down this road before often experience various degrees
of whiplash effect. Some will begin treating more integrated tests with extreme
prejudice. Others will swear off testing altogether. Short of that, there are a
few things teams might consider when planning their testing strategy:

1. Rather than write a test for each discrete layer of an application, decide in
   advance to only explicitly test a subset of those layers (in Part 4's [The
   Middle of the Pyramid](part-4-where-to-test/the-middle-of-the-pyramid.md),
   we'll look at how to choose which layers to test)
2. Because frameworks are usually the reason applications have highly-layered
   architectures, consider leaving the framework-coupled bits to be tested only
   by a single suite of highly-integrated tests. This will pressure the team to
   extract most meaningful business logic outside the layers imposed by the
   framework
3. Consider writing isolated unit tests that replace their dependencies on
   lower-level units with fakes. In that way, each test will be coupled to its
   _contract_ with the lower level, as opposed to the _behavior_ of all the
   layers beneath it
4. Instead of assuming each story should necessitate an additional integration
   test, strive to maintain as small a set of integration tests as can possibly
   exercise every feature. Some people have called these "[journey
   tests](https://martinfowler.com/bliki/UserJourneyTest.html)"

There are certainly other strategies to avoid this particular pain point, but
more useful than any strategy is this mindset: if writing a test ever feels like
a rote exercise, it's probably also an unnecessary one. That sense of boredom can
serve as useful feedback that perhaps the testing strategy or the application
architecture can be reworked. If every feature requires developers to tell the
computer the same eighty things, perhaps there's a way to make the computer do
that work for us.

## Recovering from redundant coverage

So, what can a team do once it realizes that it's tested itself into a corner?
There is no easy solution, but every way out depends on reframing their
perspective on testing. Instead of viewing every test as inherently good and
worthwhile, the value each test provides must be weighed against its costs. This
usually starts with loosening any compunction over allowing zero defects to slip
into production.

Most teams that find themselves with a hard-to-maintain, highly-redundant test
suite operate on the assumption that mean-time-to-failure (that is, a bug
reaching production) is the only measure of quality. After all, minimizing the
number of calls from angry customers over a software defect seems like a
laudable goal. However, no test suite could ever catch _every_ defect, because
bugs themselves are social constructs defined in part by fallible interpersonal
communication and variations in perception about the system's desired behavior.

Once a team is willing to admit that no test suite can hope to catch _every_
bug, then the value of mean-time-to-resolution (how fast the team can resolve
issues) may become more apparent. If a non-zero number of angry customer calls
are accepted as a fact of life, then being able to respond quickly and
effectively is something by which the team should also be measured. Through that
lens, redundant test suites seek to maximize mean-time-to-failure, but often at
the cost of inadvertently increasing mean-time-to-resolution. This realization
may dispel the belief that all test code is an unimpeachable good.

So, what can a team with a very slow, highly-redundant test suite do to recover?
For starters:

1. First, stop the bleeding and adopt whatever preventative measures (like the
   ones enumerated above) are appropriate for the given situation
2. Start clocking how much time the team spends in dutiful service to its
   tests—both the time developers spend fixing them and the amount of time the
   team spends waiting on feedback from their machines and continuous
   integration builds.  Quantify the cost of this expense and ask how it
   compares to the risk of production issues that those activities might be
   preventing
3. Change the team's operational stance on test failures. When a
   course-of-business change breaks a seemingly-unrelated test, pause before
   rushing to fix it. Force the question of whether the test provides enough
   value to justify the expense of continuing to maintain it
4. Identify tests that have never or only very rarely fail, then batch them into
   a secondary build that runs less frequently and doesn't block production
   releases. A test that never fails tells you just as little as a test that's
   always broken
5. When a test fails, start keeping score on whether it was a true negative (the
   failure indicated a bug to be fixed in the code) or a false negative (the
   failure necessitated a change to the test). Nominate tests for deletion whose
   failures are dominated by false negatives
6. Run a code coverage report of the entire build and sort by "hits per line",
   to determine which parts of the code are invoked most. Use this as a guide
   for nominating tests (or classifications of tests) for deprioritization or
   deletion
7. Begin replacing the confidence generated by automated tests by investing in
   other confidence builders, like good manual testing

Teams can recover from this dilemma, but progress will almost certainly be
frustratingly gradual. We are now living in an era where slow, hard-to-maintain
test suites are a major impetus for rewriting entire systems. Approaches like
those listed above can reliably improve most situations, but there may be cases
where a partial or complete rewrite would be more cost-effective than gradual
remediation.


