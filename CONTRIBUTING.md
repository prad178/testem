Contributing to Testem
======================

Open source is all about DIY! If you want something fixed, it's sometimes faster to just roll your sleeves up, not to mention lots more rewarding. This doc will give you some pointers on where to look when you poke around Testem's source code.

Getting Started
---------------

* Fork and checkout [github.com/testem/testem](https://github.com/testem/testem)
* Run `npm install` and `npm test` to make sure you're off to a good start

> Testem expects `PhantomJS` to be in the PATH, if you don't have one,
> either install it globally via `npm install -g phantomjs`
> (*you might need to use `sudo` for global installiation*)
> or run `npm run install:all` instead of `npm install` during the second step

Brief Code Walk Through
-----------------------

`testem.js` is the main entry point of the program. It then delegates to either `lib/dev/index.js` or `lib/ci/index.js` depending on whether it's development mode `testem` or continuous integration mode `testem ci`. All of the rest of the Node application's source is under the `lib` folder. You can probably figure out the rest from there.

The source code for the browser side is under the folders `public/testem` and `views`

* `public/testem` - is where the client side assets are (Javascript and CSS)
* `views` - are HTML templates used to generate default test runner pages

Debug Mode
----------

Use the `-d` flag to turn on debug mode. This will allow you to use

    log.info('some log message')

To log to the debug log, which is `testem.log`. If the `log` is not present in a module file, just require npmlog like so at the top of the file

    var log = require('npmlog')

Then, in a separate terminal you can tail the log and monitor debug messages

    tail -f testem.log

Tests and Examples
------------------

To maximize the chances of your pull request getting merge, you should go with a test-first approach. That means:

1. write a failing test that demonstrates the bug or lack of feature
2. fix bug or implement feature, getting the test to pass

To run the tests:

    npm test

Or in the spirit of eating our own dog food:

    testem

To lint your code:

    npm run lint

If it isn't practical to write a test first, it might be my fault, feel free to chat.

*Protip: to make the tests run faster during TDD, use Mocha's exclusive test feature, i.e. `describe.only` and `it.only`.*


### Integration Tests

There are also some integrations tests that test running all the examples in the `examples` folder by cd'ing into each and executing `testem ci`

Node + PhantomJS

    npm run integration

All available browsers (launchers)

    npm run integration:all
