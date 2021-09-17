### Pytest Tornado conflict with Nameko

This repo is a minimal reproduction of a deadlock issue I'm having with Pytest while using [nameko](https://github.com/nameko/nameko) package.

The project uses Tornado as a HTTP server. The issue happens when trying to test an endpoint. It seems that calling `eventlet.monkey_patch()` as soon as possible could be the cause of the issue. 

In this reproduction, notice that no `nameko` code is being used. A simple integration test is the only code added (see `main_test.py`).

#### How to run it

1. Using [pipenv](https://pipenv.pypa.io/en/stable/), run: `pipenv install`.
2. Run pytest: `pipenv run pytest`

**Issue**: The courotine never finishes, leaving pytest on a deadlock.

#### Why nameko might be involved?

After following the instructions above, remove `nameko` package and run the tests again:

1. Remove package: `pipenv uninstall nameko`
2. Re-run tests: `pipenv run pytest`

Notice how the test immediately passes.

Squash test.