
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Useful git pre-commit hooks for R related projects

<!-- badges: start -->

[![Travis build
status](https://travis-ci.org/lorenzwalthert/pre-commit-hooks.svg?branch=master)](https://travis-ci.org/lorenzwalthert/precommit)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
<!-- badges: end -->

[Pre-commit hooks](https://pre-commit.com) are tests that run each time
you attempt to commit. If the tests pass, the commit will be made,
otherwise not. A very basic test is to check if the code is parsable,
making sure you have not forgotten a comma, brace or quote. To learn
more about available hooks and why to use them consult the [online
documentation](https://lorenzwalthert.github.io/precommit/index.html).

## Installation

Please make sure you have conda installed. The rest can be handled from
R:

``` r
# once
remotes::install_github("lorenzwalthert/precommit")
precommit::install_precommit()

# in every project
precommit::use_precommit()
```

This installs pre-commit and performs some other set-up tasks. If you
want more control over the installation, see
`vignette("manual-installation")`.

# Usage

The next time you run `git commit`, the hooks listed in your
`.pre-commit-config.yaml` will get executed before the commit. The
helper function `precommit::open_config()` let’s you open the
`.pre-commit-config.yaml` conveniently from the RStudio console. When
any file is changed due to running a hook, the commit will fail. You can
inspect the changes introduced by the hook and if satisfied, you can
attempt to commit again. If all hooks pass, the commit is made. You can
also [temporarily disable
hooks](https://pre-commit.com/#temporarily-disabling-hooks). If you
succeed, it should look like this:

![](man/figures/screenshot.png)<!-- -->

See the hooks provided by this repo under `vignette("available-hooks")`.
You can also add other hooks from other repos, by extending the
`.pre-commit-config.yaml` file, e.g. like this:

``` yaml
-   repo: https://github.com/pre-commit/precommit
    rev: v1.2.3
    hooks: 
    -   id: check-added-large-files
```

To update the hook revisions, just run `pre-commit autoupdate` in your
terminal of `precommit::autoupdate()`.

# Caution

**Do not abort while hooks are running.** Non-staged changes are stashed
to a temp directory when the hooks are run and may not easily be
recovered afterwards.
