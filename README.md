Script for triggering builds on Shippable
=========================================

This repository can be deployed to Heroku to periodically trigger Shippable builds. It provides single Rake task called
`trigger_build` that takes two arguments: Shippable token and space-separated list of projects to trigger.

Supplied `shippable.yml` file outputs the API token in the Shippable console, so you can copy it to the Heroku dashboard.
It also adds Heroku Scheduler add-on, so you can define when and how to trigger the builds.

For example, you may add the following command in Heroku Scheduler dashboard to trigger project with id `abba`, using API
token `deadbeef`:

    rake trigger_build[deadbeef,abba]

To trigger projects `abba` and `mamma` in one run (note the quotes):

    rake "trigger_build[deadbeef,abba mamma]"

See [Heroku documentation](https://devcenter.heroku.com/articles/scheduler) for details on how to use Scheduler.
