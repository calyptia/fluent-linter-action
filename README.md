<p align="center">
    <a href="https://github.com/marketplace/actions/fluent-linter-action">
      <img src="https://img.shields.io/badge/Marketplace-v0.2.1-undefined.svg?logo=github&logoColor=white&style=flat" alt="GitHub Marketplace" />
    </a>
    <a href="https://github.com/calyptia/fluent-lint-action/actions/workflows/unit-tests.yml">
      <img src="https://github.com/calyptia/fluent-linter-action/actions/workflows/unit-tests.yml/badge.svg" alt="unit-tests" />
    </a>
    <a href="https://codecov.io/gh/calyptia/fluent-linter-action">
      <img src="https://codecov.io/gh/calyptia/fluent-linter-action/branch/main/graph/badge.svg?token=48gHuQl8zV" alt="codecov" />
    </a>
    <a href="http://slack.fluentd.org/">
      <img src="https://img.shields.io/badge/slack-@slack.fluentd.org-green.svg?logo=slack" alt="Slack" />
    </a>
    <a href="https://github.com/calyptia/fluent-linter-action/blob/main/LICENSE">
      <img src="https://img.shields.io/github/license/calyptia/fluent-linter-action" alt="APACHE 2.0 license" />
    </a>
</p>

<p align="center">
  <a href="https://github.com/calyptia/fluent-linter-action">
    <img src="logo.svg" alt="Logo" width="95" height="105">
  </a>

  </p>

## Table of Contents 🦉

- [Getting Started](#getting-started)
- [Installation](#installation)
  - [Add workflow to your repository](#add-workflow-to-your-repository)
    - [Using GitHub UI](#using-github-ui)
    - [Manual](#manual)
  - [Get Calyptia API Key](#get-calyptia-api-key)
  - [Configure secret in your repository](#configure-secret-in-your-repository)
- [Limitations](#limitations)
- [Contributing](#contributing)
- [License](#license)

# Getting started

Fluent Bit and Fluentd configurations are simple to use. Over time, the use of these configurations will grow and complexity with it. This action will help stay away from common pitfalls. It will add linting to your development process through workflows.

# Installation

The following are steps to set up fluent linter action in your repository.

## Add workflow to your repository

The first step is to create the workflow in your repository. We describe two ways: via [Github UI](#using-github-ui) or [manually](#manual).

### Manual

1. Create the following directory in your repository `.github/workflows/`
1. Under `.github/workflows/` create a file called `fluent-linter.yml`
1. Open `.github/workflows/fluent-linter.yml`
1. paste the following content:

   ```yml
   on: pull_request

   name: Fluent-linter
   jobs:
     lint:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v2
         - id: fluent_linter_action
           uses: calyptia/fluent-linter-action@main
           with:
             calyptia-api-key: ${{ secrets.CALYPTIA_API_KEY }}
             follow-symbolic-links: 'true' # this is optional. It defaults to false.
             config-location-glob: '*.conf'
   ```

1. Make sure to change `config-location-glob` to a [glob](<https://en.wikipedia.org/wiki/Glob_(programming)>) that points to your `Fluentd` and `Fluent Bit` configuration within the repository. You can use [this page](https://globster.xyz/) to make sure your glob will match the necessary files.

_If you want to see it in action, take a look at the [example here](https://github.com/calyptia/fluent-linter-action/pull/9)_

### Using GitHub UI

1. Go to the repository you wish to add the fluent-linter-action workflow.
1. Under the tab _Actions_ look for a button called _New workflow_.
1. Under _Choose workflow_, you will find a text box. Please type "fluent-linter"
1. You will find Fluent-linter-action by Calyptia. Look for a button called "Configure"
1. Make sure to change `config-location-glob` to a [glob](<https://en.wikipedia.org/wiki/Glob_(programming)>) that points to your fluentd and fluent-bit configuration within the repository.

If everything goes well, you will see an editor that will let you change anything on the workflow before committing. You can change the version from `main` to a specific one.

_Make sure to commit the workflow to your repository._

_For more information about using workflows, take a look at\ [github documentation](https://docs.github.com/en/actions/learn-github-actions/using-starter-workflows)_

If these instructions are not working for you, you can try the [Manual approach](#Manual)

## Get Calyptia API Key

In order to get the full linting capabilities from this action, you will need to get a Calyptia token. The token is easy to get. Head over to [Calyptia Cloud](https://cloud.calyptia.com/) and log in (you can use your GitHub account). On the left panel, find _Account > settings > Generate API key_. Give a recognizable name for safekeeping (you could name it _linter_). Please copy this token.

## Configure secret in your repository

The last step will be to use the API Key we generated in Calyptia Cloud.

Add a new secret to your repository find _Settings > Secrets > New repository secret_. The name for this secret should be `calyptia-api-key`. Paste the secret you obtained in the step before.

> note: Settings is often next to the insights tab. If you can't see the option, you are missing permissions.

# Limitations

- The current `fluent-linter-action` only works with `Fluent Bit` configurations. `Fluentd` configurations will be available shortly.
- The current `fluent-linter-action` uses the latest master branch of `Fluent Bit` to run the checks. Please follow [this issue](https://github.com/calyptia/fluent-linter-action/issues/18) for updates.
- The current `fluent-linter-action` does not support ignoring or excluding any configuration from linting. Please follow [this issue](https://github.com/calyptia/fluent-linter-action/issues/19) for updates. Be aware of this if using custom plugins or images/builds which may use invalid configuration options from the point of view of the main Fluent Bit version.

<!-- CONTRIBUTING -->

## Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<!-- LICENSE -->

## License

Distributed under the Apache-2.0 License. See `LICENSE` for more information.
