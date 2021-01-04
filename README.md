## BehatHtmlFormatterPlugin

Behat 3 extension for generating HTML reports from your test results.
This fork was created as the originial had many issues to be resolved and I've resolved in a fairly hacky way.
So if you are interested in a version that works for these major areas:
 * Background Steps
 * Scenario Outlines
 * Data Tables 
 * (and more minor issues)

Then you are welcome ot use this to provide reporting right away.
As some of the hacks rely on exact behat formatting I should advise I'm using the default formatting from PHPStorm, described by this for Visual Studio code:

```json
{
     "cucumberautocomplete.strictGherkinCompletion": true
     "cucumberautocomplete.formatConfOverride": {
         "Background:": 0,
         "Scenario": 0,
         "Scenario Outline": 0,
         "Given": 2,
         "When": 3,
         "Then": 3,
         "And": 4,
         "But": 2,
         "Examples:": 2,
         "\\*": 0,
         "\\|": 4
         "#": 2
     },
}
```


### Twig report

![Twig Screenshot](http://i.imgur.com/o0zCqiB.png)

## How?

* The tool can be installed easily with composer.
* Defining the formatter in the `behat.yml` file
* Modifying the settings in the `behat.yml`file

## Installation

### Prerequisites

This extension requires:

* PHP 5.3.x or higher
* Behat 3.x or higher

### Through composer

The easiest way to keep your suite updated is to use [Composer](http://getcomposer.org>):

#### Install with composer:

```bash
$ composer require --dev swaibar/behat-html-formatter
```

#### Install using `composer.json`

Add BehatHtmlFormatterPlugin to the list of dependencies inside your `composer.json`.

```json
{
    "require": {
        "behat/behat": "3.*@stable",
        "swaibar/behat-html-formatter": "0.1.*",
    },
    "minimum-stability": "dev",
    "config": {
        "bin-dir": "bin/"
    }
}
```

Then simply install it with composer:

```bash
$ composer install --dev --prefer-dist
```

You can read more about Composer on its [official webpage](http://getcomposer.org).

## Basic usage

Activate the extension by specifying its class in your `behat.yml`:

```json
# behat.yml
default:
  extensions:
    emuse\BehatHTMLFormatter\BehatHTMLFormatterExtension:
      name: html
      renderer: Twig,Behat2
      file_name: Index
      print_args: true
      loop_break: true  formatters:
```

### Command line options

Add the following to your behat command to print a report:

`behat --format html --out MYDIRECTORY`

Setting the format to html will output the various reports that you configure below (Behat2, Twig, Minimal, etc.)

You MUST specify the output directory for the reports as MYDIRECTORY.

## Configuration

### Formatter configuration

* `output_path` - The location where Behat will save the HTML reports. Use `%paths.base%` to build the full path.

### Extension configuration

* `renderer` - The engine that Behat will use for rendering, thus the types of report format Behat should output (multiple report formats are allowed, separate them by commas). Allowed values are:
 * *Behat2* for generating HTML reports like they were generated in Behat 2.
 * *Twig* A new and more modern format based on Twig.
 * *Minimal* An ultra minimal HTML output.
* `file_name` - (Optional) Behat will use a fixed filename and overwrite the same file after each build. By default, Behat will create a new HTML file using a random name (*"renderer name"*_*"date hour"*).
* `print_args` - (Optional) If set to `true`, Behat will add all arguments for each step to the report. (E.g. Tables).
* `print_outp` - (Optional) If set to `true`, Behat will add the output of each step to the report. (E.g. Exceptions).
* `loop_break` - (Optional) If set to `true`, Behat will add a separating break line after each execution when printing Scenario Outlines.

## Issue Submission

When you need additional support or you discover something *strange*, feel free to [Create a new issue](https://github.com/swaibar/BehatHtmlFormatterPlugin/issues/new) and of course a pull request!.
