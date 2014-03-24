# Generic JMeter test #

I put together a simple JMeter test framework with start scripts for Linux/Unix/Solaris/OSX and Windows.

It consists of a JMeter Testplan `test.jmx` which is configured using a properties file `test.properties`.
The Test supports 4 threadgroups which can be configured individually.

The main goal is to save time using the Testplan out-of-the-box and only change the properties file since modifying the Testplan XML is tedious work.

## Why should you use it? ##

 * It's easy to use and easily configurable.
 * Everything you will have to do is adapt the `test.properties`
 * You won't have to change the test if you want to test different websites/web applications.
 * All you need is a host to test and at least one URL list.
 * All settings can be individually set for all threadgroups so that one threadgroup could test articles, one overview pages and another one images. Currently, 4 different threadgroups are implemented. If you want to use more threadgroups, just copy a whole threadgroup configuration and duplicate a threadgroup in the Testplan.
 * You can start the test locally or remotely on JMeter servers if you want to.
 * This test also works with the [JMeter Maven Plugin][1]. See the [JMeter Maven Plugin Example][5] test.

## Contents ##

 * `example/` -> contains an example configuration for a test against mozilla.com. See separate README.md
 * `windows-scripts/` -> contains command line scripts for Windows. See separate README.md
 * `test.conf` -> configuration for the test.sh script
 * `test.jmx` -> the JMeter Testplan
 * `test.properties` -> configuration blueprint for the JMeter test
 * `test.sh` -> start the test with this script.

## Preparation ##

### Software ###

 * Download and extract [JMeter][2]
 * Set the environment variable `JMETER_BIN` to the bin directory of the jmeter installation you just extracted.

### Linux/Unix

A shell script is included that is tested thoroughly and which supports all modes (remote jmeter servers, local with GUI, local without GUI)

You can either modify the config file `test.conf` to fit your needs, or pass all parameters via command line:

    bash$ ./test.sh -h
    usage: test.sh [arguments] [-p test.properties]

    Example: test.sh -d

    Arguments:
        -h: displays this help text.
        -d: produce debug output
        -g: start jmeter GUI, you'll have to start the test manually
        -j: use jmeter servers instead of local jmeter instance
        -p: propertyfile to use for test run. Default: test.properties
    Version: 1.0

The shell script will automatically generate `log/` and `report/` folders and output files.

### Windows

See scripts and description in `windows-scripts/` folder.

## URL lists ##

The URLs in the file have to be relative to the hostname.

You could use a website crawler/broken link checker to generate a URL list for your test content. Possible tools:

 * Windows/Linux (using Wine): [Xenu's link sleuth][3]
 * Mac OSX: [Integrity][4]

## Using JMeter GUI ##

 * If you run the test with GUI, the results will NOT be written to the result.csv file automatically.

In GUI mode, you have several options.

### There are four Result Processors which are deactivated: ###

 * `Results Tree` -> Show each request, with response, status, assertions ...
 * `Summary Report` -> Shows just a summary across all requests
 * `Simple Data Writer` -> Writes the results to a csv file
 * `Graph Results` -> Shows the requests as dots, with average. Can be saved as a picture.

You can easily enable each of the processors by right clicking on the node and selecting **enable**

If you changed something like activating a Request Processor:

**After you are done testing and you close JMeter, do not save changes to the test file as it suggests!**

[1]:    http://jmeter.lazerycode.com                                "JMeter Maven Plugin"
[2]:    http://jakarta.apache.org/jmeter/                           "JMeter"
[3]:    http://home.snafu.de/tilman/xenulink.html                   "Xenu's link sleuth"
[4]:    http://peacockmedia.co.uk/integrity/                        "Integrity"
[5]:    https://github.com/afranken/jmeter-maven-plugin-example     "JMeter Maven Plugin Example"


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/afranken/generic-jmeter-test/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

