Script for triggering builds on Shippable
=========================================

This repository can be deployed to Heroku to periodically trigger Shippable builds. It provides single Rake task called
`trigger_build` that takes list of GitHub repos to trigger builds for.

The Rake task expects environment variable called `GITHUB_API_KEY` that contains access token for
GitHub API. Please refer to
[GitHub documentation](https://help.github.com/articles/creating-an-access-token-for-command-line-use)
on how to generate one. For security reasons, we recommend to not include this token in your
source code repository. Instead, add a secure variable with the same name to the `shippable.yml`.
The configuration will be exported to Heroku in `after_success` step.

Supplied `shippable.yml` file adds Heroku Scheduler add-on, so you can define when and how to trigger the builds.

For example, you may add the following command in Heroku Scheduler dashboard to trigger project from
repository `Shippable/shippable-build-trigger`:

    rake trigger_build[Shippable/build-trigger]

To trigger multiple builds, separate repository names with space, enclosing the argument in quotes:

    rake "trigger_build[Shippable/build-trigger Shippable/sample-ruby-mongo-heroku]"

You can check for results of the script execution by running `heroku logs`.

Please note that the build will be triggered for the `master` branch.
See [Heroku documentation](https://devcenter.heroku.com/articles/scheduler) for details on how to use Scheduler.
