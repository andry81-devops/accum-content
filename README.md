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
  <a href="https://github.com/andry81/donate"><img src="https://github.com/andry81-cache/andry81--gh-content-cache/raw/master/common/badges/donate/donate.svg" valign="middle" alt="donate" /></a>
</p>

---

## Tutorial to setup accumulation of various external statistic and content

> **Warning** This tutorial does contain content related to not the GitHub itself.
>

Other tutorials:

* https://github.com/andry81-devops/github-accum-stats

* https://github.com/andry81-devops/github-action-extensions

**Features**:

1. Implementation can accumulate external inpage downloads (track counter), phpbb forum board view/replies (track counters), external content (svg files, images, etc) into a cache repository.

2. Workflow has used a bash script to accumulate statistic:

   * External inpage downloads: [accum-downloads.sh](https://github.com/andry81-devops/gh-workflow/blob/master/bash/inpage/accum-downloads.sh)

   * PhpBB forum board views/replies: [accum-stats.sh](https://github.com/andry81-devops/gh-workflow/blob/master/bash/board/accum-stats.sh)

   * External content cache: [accum-content.sh](https://github.com/andry81-devops/gh-workflow/blob/master/bash/cache/accum-content.sh)

3. Basically most of the scripts does accumulate the response. For example, the board viewes/replies accumulator script does accumulate statistic both into a single file: `traffic/board/myboard/latest.json`,
   and into a set of files grouped by year and allocated per day: `traffic/board/myboard/by_year/YYYY/YYYY-MM-DD.json`.

4. You can directly point the statistic or the content cache as a standalone commits list: `https://github.com/{{REPO_OWNER}}/{{REPO}}--gh-stats/commits/master/traffic/clones` or `https://github.com/{{REPO_OWNER}}/{{REPO}}--gh-content-cache/commits/master`.

5. All scripts does use GitHub composite action to reuse workflow code base: https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

> **Warning** Not all features of a generic GitHub action is supported: [Known Issues](#known-issues)

You need setup 2-5 repositories:

1. Repository, where content config file will be stored: `myrepo--gh-content-config`.<br />
   > **Note** This repository is only required for the content accumulation script. This repository and a content store repository can be a single.

2. Repository, where to store downloaded content: `myrepo--gh-content-cache`.<br />
   > **Note** This repository is only required for the content accumulation script. This repository and a content config repository can be a single.

   **Features of a standalone content cache repository**:

   * Can be extracted content not related to a specific repository or related to multiple repositories from a target repository.

   * Extracted content can be updated separately from a target repository. For example, after a release commit into a target repository.

   * Traffic to an external resource can be replaced by traffic to the GitHub resource with better caching.

   * All content can be stored in a single place and content change be saved into a commits list.

   * Download and accumulate process can be controlled by explicit config file with parameters (can be outside of a content cache repository).

   * The content cache repository can be rewrited to remove old files and history does not touching anything else.

3. Repository, where statistic will be saved: `myrepo--gh-stats`.<br />
   > **Note** This repository is only required for the statistic accumulation script.

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

> **Note** You need to attach a personal access token (PAT) into a repository used to run a GitHub action script (`.github/workflows/*.yml`) to read content from another repository and obtain the read permission from that repository: `repo`->`public_repo`.

> **Note** You need to attach a personal access token (PAT) into a repository used to run a GitHub action script (`.github/workflows/*.yml`) to write content into another repository and obtain the push permission into that repository: `repo`.

> **Note** A separate personal access token (PAT) does not require to be attached into a repository used to run a GitHub action script for another repository as long as that another repository is owned by the same owner as a repository which runs a GitHub action script.

* `myrepo--gh-stats` -> needs read/write content permission
* `myrepo--gh-content-config` -> needs read content permission
* `myrepo--gh-content-cache` -> needs read/write content permission

To generate PAT: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token

To attach PAT: https://docs.github.com/en/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository

The `myrepo-*` repository should contain 1 file per statistic entity:

* [.github/workflows/accum-mypage-download-stats.yml example](https://github.com/andry81-devops/gh-action--accum-inpage-downloads#accum-mypage-download-stats-yml)

* [.github/workflows/accum-phpbb-board-stats.yml example](https://github.com/andry81-devops/gh-action--accum-board-stats#accum-phpbb-board-stats-yml)

* [.github/workflows/accum-content.yml example](https://github.com/andry81-devops/gh-action--accum-content#accum-content-yml)

> **Warning** You must replace all placeholder into respective values:

* `{{REPO_OWNER}}` -> repository owner
* `{{REPO}}` -> `myrepo-*`

After the github workflow yaml file is commited and pushed, you can run the action from the `Actions` tab in the `myrepo-*` repository.

> **Note** See <a href="https://github.com/andry81-devops/github-accum-stats#reuse">REUSE</a> section for details if you have multiple repositories and want to store all GitHub workflow scripts (`.github/workflows/*.yml`) in a single repository.

## Known Issues

https://github.com/andry81-devops/github-accum-stats#known-issues

## Last known issues updates

https://github.com/andry81-devops/github-accum-stats#last-known-issues-updates
