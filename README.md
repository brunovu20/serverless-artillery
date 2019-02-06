# serverless-artillery [![Build Status](https://travis-ci.org/Nordstrom/serverless-artillery.svg?branch=master)](https://travis-ci.org/Nordstrom/serverless-artillery) [![Coverage Status](https://coveralls.io/repos/github/Nordstrom/serverless-artillery/badge.svg?branch=master)](https://coveralls.io/github/Nordstrom/serverless-artillery?branch=master)

[//]: # (Thanks to https://www.divio.com/en/blog/documentation/)

Serverless-artillery makes it easier to test services for load and functionality more quickly and with almost no code.


### Use serverless-artillery if

1. You want to know if your services (either internal or public) scale with a different amount of traffic.
1. You want to test if your services behave as you expect after you deploy new changes
1. You want to constantly monitor your services over time to make sure the latency of your services is under control.


### Installation

Before installing serverless-artillery, you will need to get the latest version of node at https://nodejs.org/en/download/ or with your operating system’s package manager.

Now you can install serverless and serverless-artillery:
```
npm install -g serverless
npm install -g serverless-artillery
```
If this didn’t work, read [problems installing serverless-artillery](https://github.com/Nordstrom/serverless-artillery/blob/monitoring-mode/root-owns-node-modules.md).

### Tutorial

Let’s learn by example.

Throughout this tutorial we will walk you towards testing the AWS website, https://aws.amazon.com/.  

You can verify that serverless-artillery is installed by typing `slsart --version` from your shell; you should see something like:

```
slsart --version
0.3.2
```

Create the initial script you will need by typing the following in your shell:

```
slsart script
```

`slsart script` created script.yml file, if we look at what it contains:

```
# Thank you for trying serverless-artillery!
# This default script is intended to get you started quickly.
# There is a lot more that Artillery can do.
# You can find great documentation of the possibilities at:
# https://artillery.io/docs/
config:
  # this hostname will be used as a prefix for each URI in the flow unless a complete URI is specified
  target: "http://aws.amazon.com"
  phases:
    -
      duration: 5
      arrivalRate: 2
scenarios:
  -
    flow:
      -
        get:
          url: "/"

```

In this script, we specify that we are testing the service running on http://aws.amazon.com which will be talking to over HTTP. We define one load phase, which will last 5 seconds with 2 new virtual users (arriving every second (on average).
For more details on setting up scripts read Artillery’s documentation.

Next you want to deploy your code to aws, and you will need to set up an AWS account and set up your credentials.

With that done, you are now ready to deploy your script and start the test.

```
slsart deploy //deploys code from your computer to AWS
Slsart invoke /starts the test by creating traffic against the sample endpoint

```

After the test is done, you can remove the project from AWS:

```
slsart remove
```
