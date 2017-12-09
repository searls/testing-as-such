Suppose we are writing an HTTP
service that depends on a relational database, some internal libraries installed
as Node.js modules, and a third-party HTTP API. If we set out to test the
behavior of the HTTP service as we've defined it, then this experimental control
framing can make quick work of answering the question of what should be real and
what should be fake:

* Ideally, the subject is invoked by sending HTTP requests,
inspecting HTTP responses

If we can articulate what we hope to
observe in a test subject (say, the behavior of an HTTP service)


