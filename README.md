<p align="center">
  <a href="https://github.com/andry81-stats/accum-content--gh-stats/commits/master/traffic/views">
    <img src="https://github.com/andry81-cache/andry81-devops--gh-content-cache/raw/master/repo/andry81-devops/accum-content/badges/traffic/views/all.svg" valign="middle" alt="GitHub views|any|total" />
    <img src="https://github.com/andry81-cache/andry81-devops--gh-content-cache/raw/master/repo/andry81-devops/accum-content/badges/traffic/views/all-14d.svg" valign="middle" alt="GitHub views|any|14d" /></a>
• <a href="https://github.com/andry81-stats/accum-content--gh-stats/commits/master/traffic/views">
    <img src="https://github.com/andry81-cache/andry81-devops--gh-content-cache/raw/master/repo/andry81-devops/accum-content/badges/traffic/views/unq.svg" valign="middle" alt="GitHub views|unique per day|total" />
    <img src="https://github.com/andry81-cache/andry81-devops--gh-content-cache/raw/master/repo/andry81-devops/accum-content/badges/traffic/views/unq-14d.svg" valign="middle" alt="GitHub views|unique per day|14d" /></a>
</p>

<p align="center">
  <a href="https://github.com/andry81-stats/accum-content--gh-stats/commits/master/traffic/clones">
    <img src="https://github.com/andry81-cache/andry81-devops--gh-content-cache/raw/master/repo/andry81-devops/accum-content/badges/traffic/clones/all.svg" valign="middle" alt="GitHub clones|any|total" />
    <img src="https://github.com/andry81-cache/andry81-devops--gh-content-cache/raw/master/repo/andry81-devops/accum-content/badges/traffic/clones/all-14d.svg" valign="middle" alt="GitHub clones|any|14d" /></a>
• <a href="https://github.com/andry81-stats/accum-content--gh-stats/commits/master/traffic/clones">
    <img src="https://github.com/andry81-cache/andry81-devops--gh-content-cache/raw/master/repo/andry81-devops/accum-content/badges/traffic/clones/unq.svg" valign="middle" alt="GitHub clones|unique per day|total" />
    <img src="https://github.com/andry81-cache/andry81-devops--gh-content-cache/raw/master/repo/andry81-devops/accum-content/badges/traffic/clones/unq-14d.svg" valign="middle" alt="GitHub clones|unique per day|14d" /></a>
</p>

<p align="center">
  <a href="https://github.com/andry81/donate"><img src="https://github.com/andry81-cache/gh-content-static-cache/raw/master/common/badges/donate/donate.svg" valign="middle" alt="donate" /></a>
</p>

---

## Tutorial to setup accumulation of various external statistic and content

> [!WARNING]
> This tutorial does contain content related to not the GitHub itself.

All tutorials: https://github.com/andry81/index#tutorials

## Features:

1. Implementation can accumulate external inpage downloads counter, phpbb forum board view/replies counters, external content (svg files, images, etc) into a cache repository.

2. The workflow does use a bash script to accumulate statistic for:

   * External web page with downloads counter: [accum-downloads.sh](https://github.com/andry81-devops/gh-workflow/tree/HEAD/bash/inpage/accum-downloads.sh)

   * PhpBB forum board views/replies counter: [accum-stats.sh](https://github.com/andry81-devops/gh-workflow/tree/HEAD/bash/board/accum-stats.sh)

   * External content cache files: [accum-content.sh](https://github.com/andry81-devops/gh-workflow/tree/HEAD/bash/cache/accum-content.sh)

3. Basically most of the scripts does accumulate the response. For example, the board viewes/replies accumulator script does accumulate statistic both into a single file: `traffic/board/myboard/latest.json`,
   and into a set of files grouped by year and allocated per day: `traffic/board/myboard/by_year/YYYY/YYYY-MM-DD.json`.

4. You can directly point the statistic or the content cache as a standalone commits list: `https://github.com/{{REPO_OWNER}}/{{REPO}}--gh-stats/commits/master/traffic/clones` or `https://github.com/{{REPO_OWNER}}/{{REPO}}--gh-content-cache/commits/master`.

5. All scripts does use GitHub composite action to reuse workflow code base: https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

> [!WARNING]
> Not all features of a generic GitHub action is supported: [Known Issues](#known-issues)

## Repositories:

You need setup 2-5 repositories.

1. Repository, where content config file will be stored: `myrepo--gh-content-config`.<br />
   > [!NOTE]
   > This repository is only required for the content accumulation script. This repository and a content store repository can be a single.

2. Repository, where to store downloaded content: `myrepo--gh-content-cache`.<br />
   > [!NOTE]
   > This repository is only required for the content accumulation script. This repository and a content config repository can be a single.

   Features of a standalone content cache repository:<br />
   https://github.com/andry81-devops/gh-action--accum-content#features-of-a-standalone-content-cache-repository

3. Repository, where statistic will be saved: `myrepo--gh-stats`.<br />
   > [!NOTE]
   > This repository is only required for the statistic accumulation script.

4. Repository, where to store github workflow support scripts: `gh-workflow`.<br />
   You can fork or use it from here: https://github.com/andry81-devops/gh-workflow

5. Repository, where to store github composite action:

   * GitHub composite action to request and accumulate downloads counter statistic from a value on a web page:<br />
     https://github.com/andry81-devops/gh-action--accum-inpage-downloads

   * GitHub composite action to request and accumulate a forum board post replies/views counter statistic:<br />
     https://github.com/andry81-devops/gh-action--accum-board-stats

   * GitHub composite action to periodically download and accumulate content into a repository:<br />
     https://github.com/andry81-devops/gh-action--accum-content

   All action scripts:<br />
   https://github.com/andry81/index#action-scripts

> [!NOTE]
> You need to attach a personal access token (PAT) into a repository used to run a GitHub action script (`.github/workflows/*.yml`) to read content from another repository and obtain the read permission from that repository: `repo`->`public_repo`.

> [!NOTE]
> You need to attach a personal access token (PAT) into a repository used to run a GitHub action script (`.github/workflows/*.yml`) to write content into another repository and obtain the push permission into that repository: `repo`.

> [!NOTE]
> A separate personal access token (PAT) does not require to be attached into a repository used to run a GitHub action script for another repository as long as that another repository is owned by the same owner as a repository which runs a GitHub action script.

* `myrepo--gh-content-config` -> needs read access permission to read repository files
* `myrepo--gh-stats` -> needs read/write access permissions to read/write repository files
* `myrepo--gh-content-cache` -> needs read/write content permission to read/write repository files

To generate PAT: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token

To attach PAT: https://docs.github.com/en/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository

The `myrepo-*` repository should contain 1 file per statistic entity:

* [.github/workflows/accum-mypage-download-stats.yml example](https://github.com/andry81-devops/gh-action--accum-inpage-downloads#accum-mypage-download-stats-yml)

* [.github/workflows/accum-phpbb-board-stats.yml example](https://github.com/andry81-devops/gh-action--accum-board-stats#accum-phpbb-board-stats-yml)

* [.github/workflows/accum-content.yml example](https://github.com/andry81-devops/gh-action--accum-content#accum-content-yml)

> [!WARNING]
> You must replace all placeholder into respective values:

* `{{REPO_OWNER}}` -> repository owner
* `{{REPO}}` -> `myrepo-*`

After the github workflow yaml file is commited and pushed, you can run the action from the `Actions` tab in the `myrepo-*` repository.

> [!NOTE]
> See <a href="https://github.com/andry81-devops/github-accum-stats#reuse">REUSE</a> section for details if you have multiple repositories and want to store all GitHub workflow scripts (`.github/workflows/*.yml`) in a single repository.

## Known Issues

https://github.com/andry81-devops/gh-known-issues#known-issues

## Last known issues updates

https://github.com/andry81-devops/gh-known-issues#last-known-issues-updates
