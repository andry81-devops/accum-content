<!-- -->
<p align="center">
  <a href="#"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fandry81%2Faccum-content&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false" valign="middle" alt="hits" /></a>
</p>
<!-- -->

<p align="center">
  <a href="https://github.com/andry81-stats/accum-content--gh-stats/commits/master/traffic/views">
    <img src="https://img.shields.io/badge/dynamic/json?color=success&label=Github%20views|all&query=count&url=https://github.com/andry81-stats/accum-content--gh-stats/raw/master/traffic/views/latest-accum.json?raw=True&logo=github" valign="middle" alt="GitHub views|any|total" />
    <img src="https://img.shields.io/badge/dynamic/json?color=success&label=14d&query=count&url=https://github.com/andry81-stats/accum-content--gh-stats/raw/master/traffic/views/latest.json?raw=True" valign="middle" alt="GitHub views|any|14d" /></a>
• <a href="https://github.com/andry81-stats/accum-content--gh-stats/commits/master/traffic/views">
    <img src="https://img.shields.io/badge/dynamic/json?color=success&label=Github%20views|unq&query=uniques&url=https://github.com/andry81-stats/accum-content--gh-stats/raw/master/traffic/views/latest-accum.json?raw=True&logo=github" valign="middle" alt="GitHub views|unique per day|total" />
    <img src="https://img.shields.io/badge/dynamic/json?color=success&label=14d&query=uniques&url=https://github.com/andry81-stats/accum-content--gh-stats/raw/master/traffic/views/latest.json?raw=True" valign="middle" alt="GitHub views|unique per day|14d" /></a>
</p>

<p align="center">
  <a href="https://github.com/andry81-stats/accum-content--gh-stats/commits/master/traffic/clones">
    <img src="https://img.shields.io/badge/dynamic/json?color=success&label=Github%20clones|all&query=count&url=https://github.com/andry81-stats/accum-content--gh-stats/raw/master/traffic/clones/latest-accum.json?raw=True&logo=github" valign="middle" alt="GitHub clones|any|total" />
    <img src="https://img.shields.io/badge/dynamic/json?color=success&label=14d&query=count&url=https://github.com/andry81-stats/accum-content--gh-stats/raw/master/traffic/clones/latest.json?raw=True" valign="middle" alt="GitHub clones|any|14d" /></a>
• <a href="https://github.com/andry81-stats/accum-content--gh-stats/commits/master/traffic/clones">
    <img src="https://img.shields.io/badge/dynamic/json?color=success&label=Github%20clones|unq&query=uniques&url=https://github.com/andry81-stats/accum-content--gh-stats/raw/master/traffic/clones/latest-accum.json?raw=True&logo=github" valign="middle" alt="GitHub clones|unique per day|total" />
    <img src="https://img.shields.io/badge/dynamic/json?color=success&label=14d&query=uniques&url=https://github.com/andry81-stats/accum-content--gh-stats/raw/master/traffic/clones/latest.json?raw=True" valign="middle" alt="GitHub clones|unique per day|14d" /></a>
</p>

<p align="center">
  <a href="https://github.com/andry81/donate"><img src="https://github.com/andry81/andry81/raw/master/badges/donate.svg" valign="middle" alt="donate" /></a>
</p>

---

## Tutorial to setup accumulation of various external statistic and content

> :warning: This tutorial does contain content related to not the GitHub itself.
>

Other tutorials:

* https://github.com/andry81-devops/github-accum-stats

* https://github.com/andry81-devops/github-action-extensions

Features:

1. Implementation can accumulate external inpage downloads (track counter), phpbb forum board view/replies (track counters), external content (svg files, images, etc) into a cache repository.

2. Workflow has used a bash script to accumulate statistic:

   * External inpage downloads: [accum-downloads.sh](https://github.com/andry81-devops/gh-workflow/blob/master/bash/inpage/accum-downloads.sh)

   * PhpBB forum board views/replies: [accum-stats.sh](https://github.com/andry81-devops/gh-workflow/blob/master/bash/board/accum-stats.sh)

   * External content cache: [accum-content.sh](https://github.com/andry81-devops/gh-workflow/blob/master/bash/cache/accum-content.sh)

3. Basically most of the scripts does accumulate the response. For example, the board viewes/replies accumulator script does accumulate statistic both into a single file: `traffic/board/myboard/latest.json`,
   and into a set of files grouped by year and allocated per day: `traffic/board/myboard/by_year/YYYY/YYYY-MM-DD.json`.

4. You can directly point the statistic or the content cache as a standalone commits list: `https://github.com/{{REPO_OWNER}}/{{REPO}}--gh-stats/commits/master/traffic/clones` or `https://github.com/{{REPO_OWNER}}/{{REPO}}--gh-content-cache/commits/master`.

5. All scripts does use GitHub composite action to reuse workflow code base: https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

> :warning: Not all features of a generic GitHub action is supported: [Known Issues](#known_issues)

You need setup 3-5 repositories:

1. Repository, where content config file will be stored: `myrepo--gh-content-config`.<br />
   > :information_source: This repository is only required for the content accumulation script.

2. Repository, where to store downloaded content: `myrepo--gh-content-cache`.<br />
   > :information_source: This repository is only required for the content accumulation script.

3. Repository, where statistic will be saved: `myrepo--gh-stats`.<br />
   > :information_source: This repository is only required for the statistic accumulation script.

4. Repository, where to store github workflow support scripts: `gh-workflow`.<br />
   You can fork or use it from here: https://github.com/andry81-devops/gh-workflow

5. Repository, where to store github composite action:

   * GitHub composite action to request and accumulate downloads statistic from a value on a web page:<br />
     https://github.com/andry81-devops/gh-action--accum-inpage-downloads

   * GitHub composite action to request and accumulate a forum board post replies and views statistic:<br />
     https://github.com/andry81-devops/gh-action--accum-board-stats

   * GitHub composite action to periodically download and accumulate content into repository:<br />
     https://github.com/andry81-devops/gh-action--accum-content

   The list of actions (`gh-action--*`):
   https://github.com/orgs/andry81-devops/repositories?q=gh-action--

> :information_source: See <a href="#reuse">REUSE</a> section for details if you have multiple repositories and want to store all GitHub workflow scripts (`.github/workflows/*.yml`) in a single repository.

> :information_source: You need to attach a personal access token (PAT) into a repository used to run a GitHub action script (`.github/workflows/*.yml`) to read content from another repository and obtain the read permission from that repository: `repo`->`public_repo`.

> :information_source: You need to attach a personal access token (PAT) into a repository used to run a GitHub action script (`.github/workflows/*.yml`) to write content into another repository and obtain the push permission into that repository: `repo`.

> :information_source: A separate personal access token (PAT) does not require to be attached into a repository used to run a GitHub action script for another repository as long as that another repository is owned by the same owner as a repository which runs a GitHub action script.

* `myrepo--gh-stats` -> needs read/write content permission
* `myrepo--gh-content-config` -> needs read content permission
* `myrepo--gh-content-cache` -> needs read/write content permission

To generate PAT: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token

To attach PAT: https://docs.github.com/en/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository

The `myrepo-*` repository should contain 1 file per statistic entity:

* [.github/workflows/accum-mypage-download-stats.yml example](https://github.com/andry81-devops/gh-action--accum-inpage-downloads#examples)

* [.github/workflows/accum-phpbb-board-stats.yml example](https://github.com/andry81-devops/gh-action--accum-board-stats#examples)

* [.github/workflows/accum-content.yml example](https://github.com/andry81-devops/gh-action--accum-content#examples)

> :warning: You must replace all placeholder into respective values:

* `{{REPO_OWNER}}` -> repository owner
* `{{REPO}}` -> `myrepo-*`

After the github workflow yaml file is commited and pushed, you can run the action from the `Actions` tab in the `myrepo-*` repository.

## <a name="reuse">REUSE</a>

https://github.com/andry81/github-accum-stats/blob/master/README.md#reuse

## <a name="known_issues">Known Issues</a>

https://github.com/andry81/github-accum-stats/blob/master/README.md#known_issues

## <a name="known_issues_updates">Last known issues updates</a>

### Updates on composite actions features:

https://github.com/andry81-devops/github-accum-stats/blob/master/README.md#composite_action_features_updates