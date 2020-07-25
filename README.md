### Pytest Tornado conflict with Nameko

This repo is a minimal reproduction of a deadlock issue I'm having with Pytest while using [nameko](https://github.com/nameko/nameko) package.

The project uses Tornado as a HTTP server. The issue happens when trying to test an endpoint. It seems that calling `eventlet.monkey_patch()` as soon as possible is the cause of the issue. In this minimal reproduction, notice that no `nameko` code is being used at all. `main_test.py` is just a very simple integration test.

#### How to run it

1. Using [pipenv](https://pipenv.pypa.io/en/stable/), run: `pipenv install`.
2. Run pytest: `pipenv run pytest`

The courotine never finishes.

#### Why nameko might be involved?

After following the instructions above, remove `nameko` package and run the tests again:

1. Remove package: `pipenv uninstall nameko`
2. Re-run tests: `pipenv run pytest`

Notice how the test immediately passes.
