# Elm UI Test Suite

There are two types of tests for Elm UI. The deterministic non-browser tests are located in `tests/` and `stylesheets/build.test.js`.

Use Node 22 and Bun 1.4.2 from the repository root:

```bash
bun install --frozen-lockfile
bun run stylesheet:check
bun run test
```

Use `bun run stylesheet` explicitly when generated stylesheet, class, or flag artifacts need to be updated.

# Layout Testing

`elm-ui` also needs to ensure that all layouts work as expected on all browsers.

In order to do this, we need a different testing environment.

So, the tests in `elm-ui/tests-rendering/src/Tests` will render output, then harvest bounding boxes form the browser, and run the test on the resulting data.

Run this locally via:

```bash
bun install --frozen-lockfile
bun run test-render
```

**Note** if you run this, it runs by default in headless chrome, so you won't see a browser actually open.  Ideally you'll just see something like this:

```
Compiling tests
Done compiling
Running locally on Chrome...
Local Chrome -> All 18029 tests passed
```

That's right. We have 18,029 tests. Woohoo!

# Running on Sauce Labs

In order to automate some of this stuff, this test can be run on Sauce Labs.

If you have an account, you'll need to create a `elm-ui/sauce.env` file, which has the following fields:

```
export SAUCE_ACCESS_KEY={your key}
export SAUCE_USERNAME={your username}
```

You can then run.

```bash
bun run test-render-sauce
```

**Note**: The compiled `elm-ui` test needs to be made public somewhere in order for this to work.  At the moment it's at my github.io account, though something more permanenet might be set up.


# Sauce Labs References

https://wiki.saucelabs.com/display/DOCS/Platform+Configurator#/
https://wiki.saucelabs.com/display/DOCS/Sauce+Labs+Basics
https://github.com/saucelabs-sample-test-frameworks/Python-Pytest-Selenium
