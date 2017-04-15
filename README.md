# 🐙👒 - octohatrack

[![Travis](https://img.shields.io/travis/LABHR/octohatrack.svg)](https://travis-ci.org/LABHR/octohatrack)
![PyPI](https://img.shields.io/pypi/v/octohatrack.svg)
![PyPI](https://img.shields.io/pypi/pyversions/octohatrack.svg)
![PyPI](https://img.shields.io/pypi/l/octohatrack.svg)
![PyPI](https://img.shields.io/pypi/implementation/octohatrack.svg)
[![Say Thanks](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/glasnt)

It's easy to see some [code contributions](https://help.github.com/articles/why-are-my-contributions-not-showing-up-on-my-profile/)
on a GitHub repo, but what about everything else?

**Octohatrack** takes a github repo name, and returns two lists: 

  - A list of all users as defined by GitHub as a contributor
  - A list of all contributors to a project 

**What is a 'GitHub contributor'?**

On any GitHub repo page, the header at the top of the file listings shows a number of commits, branches, releases and contributors. If you [click the 'contributors' link](https://github.com/LABHR/octohatrack/graphs/contributors), you get a list of users that contributed code to the master branch of the repo, ordered by the commits and lines of code contributed. This list is limited to the top 100 users

**So, what are 'all contributors', then?**

That's everyone who's worked on a GitHub project. It compiles a complete list of the GitHub-defined contributors (not just the top 100), plus everyone who's created an issue, opened a pull requests, commented on an issue, replied to a pull request, made any in-line comments on code, edited the repo wiki, or in any other way interacted with the repo. 

**`CONTRIBUTORS` file formatting**

See the bottom of [CONTRIBUTORS](https://github.com/LABHR/octohatrack/blob/master/CONTRIBUTORS) for details. 

**Limitations**

As at April 2016, there is no API endpoint for [GitHub Reactions](https://github.com/blog/2119-add-reactions-to-pull-requests-issues-and-comments), so these aren't able to be counted. [Issue #87](https://github.com/LABHR/octohatrack/issues/87)
 

**#LABHR**

"Let's All Build a Hat Rack" ([\#LABHR](https://twitter.com/search?q=%23LABHR&src=typd)) is an
original concept by [Leslie Hawthorn](http://hawthornlandings.org/2015/02/13/a-place-to-hang-your-hat/)

Read more about octohatrack:

-   [A tool for tracking GitHub contributions](https://opensource.com/life/15/10/octohatrack-github-non-code-contribution-tracker) on OpenSource.com
-   [Acknowledging Non-Coding Contributions](https://modelviewculture.com/pieces/acknowledging-non-coding-contributions) on ModelViewCulture.com
-   [Build a Better Hat Rack: All Contributions Welcome](https://www.youtube.com/watch?v=wQxFKxbWcFM) from KiwiPyCon (YouTube video)
-   [Read about the project name change](http://glasnt.com/blog/2015/11/21/goodbye-octohat.html)

## Installation

```
pip install octohatrack
```

`octohatrack` requires Python 3. Check your `pip --version` to ensure that it's pointing to a Python 3 installation. If you have both Python 2.7 and Python 3 on your system, you may need to install using: 

```
pip3 install octohatrack
```

See "Debugging: Python 3 requirement" for more information.

## Usage

```
usage: octohatrack [-h] [--no-cache] [-v] username/repo

positional arguments:
  username/repo      the name of the repo to parse

optional arguments:
  -h, --help         show this help message and exit
  --no-cache         Disable local caching of API results
  -v, --version      show program's version number and exit
```

Define an environment variable for `GITHUB_TOKEN` to use an [authentication token](https://help.github.com/articles/creating-an-access-token-for-command-line-use/) to avoide being [Rate Limited](https://developer.github.com/v3/#rate-limiting)
to 60 requests per hour (allows for deeper searching).


## Run this repo locally

```
git clone https://github.com/labhr/octohatrack
cd octohatrack
python3 -m octohatrack [arguments]
```

## Run octohatrack in a Docker container

```
git clone https://github.com/labhr/octohatrack
cd octohatrack
docker build -t octohatrack .
docker run -e GITHUB_TOKEN octohatrack [arguments]
```

## Example output

```
$ octohatrack LABHR/octohatrack

Checking repo exists.......
Getting API Contributors..................
Getting Issue and Pull Request Contributors................................................................................................................................................................................................................................................................................
Getting File Contributors.......
Getting Wiki Contributors......

All Contributors:
Anna Ossowski (ossanna16)
Christopher Hiller (boneskull)
Cory Benfield (Lukasa)
Davey Shafik (dshafik)
David Beitey (davidjb)
Deb Nicholson (baconandcoconut on twitter)
E. Dunham (edunham)
Jan Niggemann (jniggemann)
Katie McLaughlin (glasnt)
Kenneth Reitz (kennethreitz)
Kirstie Whitaker (KirstieJane)
Kristian Perkins (kristianperkins)
Laura (alicetragedy)
Lee Symes (leesdolphin)
Leslie Hawthorn (lhawthorn on twitter)
Marc Tamlyn (mjtamlyn)
Mike Sampson (mfs)
Nick Coghlan (ncoghlan)
Rogerio Prado de Jesus (rogeriopradoj)
Russell Keith-Magee (freakboy3742)
Stewart Smith (stewart-ibm)
Sumana Harihareswara (brainwane)
Sven Dowideit (SvenDowideit)
Tennessee Leeuwenburg (tleeuwenburg)
The Gitter Badger (gitter-badger)
Thomas A Caswell (tacaswell)
Thomas Winwood (Ketsuban)
Tim Groeneveld (timgws)
Tobias Kunze (rixx)
Tom Clark (tclark)

Repo: LABHR/octohatrack
GitHub Contributors: 10
All Contributors: 30 👏
```


## Debugging

### Python 3 requirement

`octohatrack` requires Python 3.

This is because there's a number of features that require Python 3, and `octohatrack` is *not* `--universal`. More specifically, there are some system utils that are Python 3 only, and Unicode support in Python 3 is **so** much easier than in Python 2.

If you are having issues installing and are getting a `octohatrack requires a Python 3 environment` error, check: 
 - `python --version`
 - `pip --version`

If you are running in an environment with both Python 2 and Python 3, you may need to use `pip3` to install. 

There are two checks in `setup.py` and `__main__.py` that will end the installation or execution, respectively, running if it doesn't detect a Python 3 environment. 


If you *are* running in a Python 3 environment and it kicks you out, please [log an issue](https://github.com/LABHR/octohatrack/issues/new), including your `python --version`, and if you're running in a virtualenv. 

### Cache

As of octohatrack 0.3.0, there is now a cache that gets created. 
Any time an external API call is made, it gets saved to a local
cache file so that any subsequent calls don't have to burn an API call.

You can disable the cache by using the `--no-cache` flag. 

To reset the cache, remove the `cache_file.json` file.

If you experience ongoing issues with the caching,
please [log a detailed issue describing what you're seeing](https://github.com/LABHR/octohatrack/issues/new)

### Wiki

Because GitHub doesn't have an API endpoint for being able to parse gollum-based repo-wikis, I've had to default to cloning repos locally and parsing via gitpython. 

If there are issues cloning the wiki, or other issues, it shouldn't break an octohatrack run, but if you do encounter issues, please [log an issue](https://github.com/LABHR/octohatrack/issues/new), and be sure to include platform information (this functionality has been tested on Mac OSX Yosemite and Ubuntu Xenial)


## To do

-   include merge-only contributors

## Code of Conduct

Octohatrack operates under a [Code of
Conduct](https://github.com/labhr/octohatrack/blob/master/code-of-conduct.md).

## License

Octohatrack is distributed under the [MIT license](https://github.com/labhr/octohatrack/blob/master/LICENSE).

This project is not affiliated with GitHub.
