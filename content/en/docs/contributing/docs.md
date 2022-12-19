---
title: Documentation
date: 2022-02-04T17:00:00+02:00
draft: false
weight: 507
---

## Documentation

As with the other parts of Unikraft, we welcome contributions to the [documentation repository](https://github.com/unikraft/docs).
Documentation is written using [GitHub Markdown](https://github.github.com/gfm/) and is built using [Hugo](https://gohugo.io/commands/hugo_server/).

Please use pull requests (PRs) to submit corrections and improvements to documentation.
You can add entire sections if you think a topic is missing or update existing ones with missing information.

You can also open up an issue to signal a problem or a missing part in the documentation that you request someone to fix.

We use English as a documentation language.
Please proofread your text before submitting a pull request.

Write each sentence on a new line.
This way, changing one sentence only affects one line in the source code.

Prefer using the 1st person plural.
Use phrases like "we run the command / app", "we look at the source code", "we provide support".

### Content Layout

The content has the following structure:

```text
content/
`-- en
    |-- blog/                   # Blog posts, <date>-<blogpost title>.md
    |
    |-- community/              # Community related content
    |   |-- contacts.md         # Community contacts
    |   |-- events.md           # Informations related to reccuring and upcoming events
    |   |-- github.md           # Unikraft GitHub community layout
    |   |-- hackathons/         # Hackathon sessions, challenges and sollutions
    |   |-- _index.md           # Community first page
    |   |-- people.md           # List of people in the community
    |   |-- publications.md     # List of Unikraft-related publications (theses, peer-reviewed publications, etc.)
    |   `-- talks.md            # List of Unikraft-related talks and presentations
    |
    |-- docs/                   # Unikraft documentation, split by categories into subdirectories
    |
    |-- faq/                    # List of frequently asked questions
    |
    `-- releases/               # Unikraft releases summaries
```

### Testing Changes

Before you submit your changes for review, please make sure you have tested it thoroughly.
You can build and deploy the site locally, following [the instructions below](/contributing/docs/#building).
You can also use the [Super Linter](https://github.com/github/super-linter), following the [instructions below](docs/contributing/docs/#using-the-linter).
Please also do a spell check on your changes.
Most text editors should be able to do that by themselves, [here's how you do it in `Vim`](https://thoughtbot.com/blog/vim-spell-checking).

#### Building the Website

You can build the website inside a Docker environment or natively.
Building inside a Docker environment is recommended, since you will work in the same environment as the deployed website.

#### Building the Website Inside a Docker Environment

You can build the site inside a Docker environment.
For this, you will need to install Docker-CE.
You can do that by following the instructions [here](https://github.com/docker/docker-install), or by running:

```console
$ curl -fsSL https://get.docker.com/ | sh
```

**Note: Building the site inside a Docker environment is highly recommended, since you will work in the same environment as the deployed site, so there will be no errors regarding packages version or filesystem layout.**

To deploy the site, run:

```console
$ make container
$ make devenv # This will take you inside the container

# Inside the container, run the following commands:
$ npm install
$ make serve
```

You may need admin privileges to run the first 2 commands.

#### Building the Website Natively

You can also build the site natively.
For a native build, you need to install `hugo`.
You can do it by following the instructions [here](https://gohugo.io/getting-started/installing/).

Then, to build and deploy the site, run:

```console
$ hugo serve
```

**Note: This may lead to errors due to different `hugo` versions or other environment problems.
The problems can be avoided by building the webside inside a Docker environment.
If you choose to build the site natively, make sure you use [`Hugo v0.98.0`](https://github.com/gohugoio/hugo/releases/tag/v0.98.0).**

After building and deploying the site, `hugo` provides instructions on accessing and using it:

```text
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
```

Access the `http://localhost:1313/` URL in the browser to view the site.

#### Using the linter

To automate a big part of the reviewing process, we use the [super linter](https://github.com/github/super-linter) on the `docs` repository.
It runs as a GitHub action on every time you do a push, checking all the changed files.

{{< img
   class="w-auto mx-auto"
   src="/assets/imgs/github-super-linter.png"
   title="Checking the super linter output"
   caption="If you open a pull request, you will be able to see the linter output under the checks section."
   position="center"
>}}

If you click on `details`, you can see the full linter output.
The most relevant part is under the `Lint Code Base` section, where you can find the full error messages and the line that generated the error.

{{< img
   class="w-auto mx-auto"
   src="/assets/imgs/github-super-linter-output.png"
   title="Checking the super linter output"
   caption="Full linter output. Error was caused by line 79 in file `content/en/blog/2022-12-03-random-device-support-in-unikraft.md`"
   position="center"
>}}

Since the linter checks the entire file, you may find yourself with a lot of errors from lines that you did not modify.
If you have the time to add a commit to your pull request that fixes all the linting errors within the modified files, we will be forever grateful :pray:
If not, please make sure that the errors are not caused by the lines that you added or modified.

**You can also run the linter locally.
Note that there is a set of linters run via super-linter.
For the Unikraft documentation repository, used and useful linters are [`markdown-cli`](https://github.com/igorshubovych/markdownlint-cli#readme), [`textlint`](https://textlint.github.io/) and [`jscpd`](https://github.com/kucherenko/jscpd).
Instructions on installing and using them are below.**

You can run the `super-linter` locally, following the instructions [here](https://github.com/github/super-linter/blob/main/docs/run-linter-locally.md).
Note that this will require quite a lot of storage, since it will pull the `super-linter` Docker image.

You will need to install Docker, following the [official documentation](https://docs.docker.com/install/).
After that, pull the latest container by running:

```console
$ docker pull github/super-linter:latest
```

To run the `super-linter` for one file, use:

```console
$ docker run -e RUN_LOCAL=true -e USE_FIND_ALGORITHM=true -v /path/to/local/codebase/file:/tmp/lint/file github/super-linter
--------------------------------------------------------------------------------
2022-12-29 07:50:55 [INFO]   ---------------------------------------------
2022-12-29 07:50:55 [INFO]   --- GitHub Actions Multi Language Linter ----
2022-12-29 07:50:55 [INFO]    - Image Creation Date:[2022-12-26T16:46:33Z]
2022-12-29 07:50:55 [INFO]    - Image Revision:[154522b380449499473f75d46f3796e23ebc1d2e]
2022-12-29 07:50:55 [INFO]    - Image Version:[154522b380449499473f75d46f3796e23ebc1d2e]
2022-12-29 07:50:55 [INFO]   ---------------------------------------------
2022-12-29 07:50:55 [INFO]   ---------------------------------------------
2022-12-29 07:50:55 [INFO]   The Super-Linter source code can be found at:
2022-12-29 07:50:55 [INFO]    - https://github.com/github/super-linter
2022-12-29 07:50:55 [INFO]   ---------------------------------------------
2022-12-29 07:50:55 [INFO]   --------------------------------------------
[...]
```

You can also run each liner separately, since it will require less storage space.
To run the linters, you will need to install the [`markdown-cli`](https://github.com/igorshubovych/markdownlint-cli), [`textlint`](https://textlint.github.io/docs/getting-started.html) and [`jscpd`](https://github.com/kucherenko/jscpd#installation) tools.

```console
$ npm install -g markdownlint-cli
$ npm install -g textlint
$ npm install -g jscpd
```

The `textlinter` will require installation of rules.
You can find a list of rules [here](https://github.com/textlint/textlint/wiki/Collection-of-textlint-rule).

```console
$ npm install -g textlint-rule-no-todo
```

To run the linters, from inside the directory you want to check, use:

```console
$ markdownlint --config <path-to-your-docs-repo-clone>/.github/workflows/config/config.json --rules <path-to-your-docs-repo-clone>/.github/workflows/rules/rules.js *.md
$ npx textlint --rule <rule-name> <file>
$ npx jscpd <path-to-source-code>
```

### Reviewing Changes

If you are assigned as a reviewer to a pull request, please follow the [testing steps](docs/contributing/docs/#testing-changes) and make sure everything looks good.

The review may go through a set of back-and-forth steps between the author and the reviewer before the reviewer marks the PR as approved.
As a reviewer, when you consider the process complete you must add a signature, in the same way that the author has.
This is done by writing adding a `Reviewed-by` line as part of your approval message in the GitHub review interface:

```text
Reviewed-by: Your Name <your@email.com>
```
