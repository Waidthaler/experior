# Experior 0.0.1
**A minimal but powerful and language-agnostic unit and regression test tool.**

> "Experior" is a Latin verb meaning "to put to the test". It is the root of the English words "experiment", "experience", and "expert".

## Overview

Experior is a Node-based command-line tool, not a library or framework. It takes 
specially marked-up test output from your test program which may have performed 
its own tests and included the results, and it generates reports in various 
formats from that. It can also apply tests written in JavaScript to the test 
output. Both types of tests can be used at the same time.

It can also emit a JSON file containing test IDs and the MD5 hashes derived from 
the test output. This can be re-used on subsequent runs to detect regressions.

Full details are below, including a tutorial with examples.

## Installation

If you're not interested in poking around with the source, the easiest thing to do
is to just use `npm` to install the Node.js module:

```bash
$ npm install experior --global
```

__Note:__ Experior is currently in beta as of 3/13/2019 and has not yet been 
published to the NPMjs repository.

## Command-Line Usage

```
===========================================================================
         Experior v0.0.1 -- Minimalist Unit/Regression Test Tool
===========================================================================

  Usage: experior [options]

    -i, --infile     <filename(s)>  Path to input file(s).
    -o, --outfile    <filename(s)>  Output file names.
    -r, --regression <filename>     Regression test input file.
    -j, --jstest     <filename>     JavaScript test module.
    -c, --css        <filename>     CSS file to use with HTML output.
    -l, --long                      Use long report format.
    -w, --width      <number>       Set width for text descriptions.
    -m, --msgprefix  <string>       Experior message prefix.
    -f, --failures                  Only show failures in reports.
    -p, --prng       <type> <num>   Generate num random numbers of type.
    -s, --seed       <num|string>   Explicit PRNG seed.
    -v, --verbose                   Increase verbosity (starts at 1, up to 4).
    -q, --quiet                     Suppress console output.
    -d, --debug                     Display debugging info.
    -h, --help                      Display this text.
```

Experior has two mutually-exclusive operating modes, testing and generation of 
test data. The latter is activated with the `--prng` switch.

### Testing Switches

When performing tests, there are two mandatory switches, `--infile` and 
`--outfile`.

__-i, --infile__: Specifies one or more input files containing test data. As with the
other switches that take multiple arguments, you can place arguments after a single instance
of a switch or use the switch multiple times, e.g.

```bash
$ experior -i foo.dat bar.dat         # is equivalent to...
$ experior -i foo.dat -i bar.dat
```

__-o, --outfile__: Specifies one or more output files whose format is determined 
by their file extensions. The supported extensions are `.txt`, `.html`, `.csv`, 
and `.json`. Additionally, you can use the special names `console` and `ansi` to 
send output to the screen. The `console` report is plain text, while the `ansi`
report uses snazzy colors.

__-r, --regression__: Specifies a JSON file generated by a previous known-good 
run to compare with the current run to detect regressions.

__-j, --jstest__: Specifies the name of a JavaScript module containing tests to
run against the test data. See the _JavaScript Tests_ section below for details.

__-c, --css__: HTML reports have their own inline styles, but if you want to 
replace it with your own, use `-c` to provide a URL for an external stylesheet.

__-l, --long__: Activates the long report format which includes detailed test 
descriptions.

__-w, --width__: For `.txt`, `console`, and `ansi` formats, sets the width of 
the description column. The default is 40 characters.

__-m, --msgprefix__: Sets an alternate message prefix for test metadata. See
the _Test File Format_ section for details.

__-f, --failures__: If used, only failed tests will appear in the reports.

__-v, --verbose__: Increases the verbosity of informational output at the 
console. May be used up to four times.

__-q, --quiet__: Turns on quiet mode, suppressing all unnecessary console 
output.

__-d, --debug__: Turns on debugging output.

__-d, --help__: Displays the usage summary above.

### Test Data Generation Switches

Experior includes the ability to generate numeric test data.

__-p, --prng__: Takes two arguments, a _type_ and the number of items to 
generate. The type may be `8`, `16`, `24`, `32`, or `64` for integers, or 
`float` for floating point numbers.

__-s, --seed__: Provides an optional seed for the random number generator. This 
can be either a number or a string.

## Test File Format

Test files consist of test output beginning and ending with specially-marked messages
to Experior. These messages begin with a standard prefix at the beginning of the line. The
default prefix is `@EXPERIOR:`, but you can choose your own with the `--msgprefix` command
line switch. The prefix is followed by a JSON string containing the test parameters.

The message at the beginning of each test looks like this:

```
@EXPERIOR: {"type":"begin","id":"TestOne","cat":"testdata","label":"A 100% successful test","desc":"This is to test total success.","jsTest":"hasNoAlpha"}
```

## Output Formats

...

## Regression Tests

...

## JavaScript Tests

...

## Tutorial and Examples

...

## Status

Experior is currently in beta as of 3/13/2019. In a week or so, when I'm done 
testing it to my satisfaction, it will 
