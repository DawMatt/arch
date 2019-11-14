# Postman Collection Runner and Capturing Responses

## Overview

A [Postman Collection Run](https://learning.getpostman.com/docs/postman/collection-runs/starting-a-collection-run/) executes a collection as a whole, verifying how a set of API calls would interact as an application intends to use them.

While not strictly required there are three additional steps you should consider to make the collection run more valuable:

1. Use [Postman Pre-Request Scripts and Test Scripts](https://learning.getpostman.com/docs/postman/scripts/intro-to-scripts/) to prepare data for individual requests, and verify the outputs of requests. These can be useful for chaining requests together by using part of the output of one request as input to the next.
2. Use [CSV or JSON data files](https://learning.getpostman.com/docs/postman/collection-runs/working-with-data-files/) to prepare unique sets of data to be used for multiple runs of a collection. Very useful for testing a range of data conditions have been adequately addressed
3. Capture the responses into text files for further analysis. Postman does not currently provide a native feature enabling this. A work around is described in the following sub-section.

Items 1 and 2 above can be combined, using a mixture of data file and API response values to construct API calls such as:

```
{{Resource}}/data/ShoppingBasket?$filter=ProductID eq '{{productID}}' and OrderedQuantity eq {{orderedQuantity}}
```

## Capturing Responses

Capturing responses requires the following steps:

1. Using a [Collection Test Script](https://learning.getpostman.com/docs/postman/scripts/intro-to-scripts/) to prepare the file output and invoke the logging API after each request is executed.
2. A simple node.js application to expose the API and write the files.

The instructions for setting this up are described in the GitHub repository. In summary:

* Install [Node.js](https://nodejs.org/en/) if you don't already have it
* Install the node.js app found in the following repository
    * https://github.com/DawMatt/ResponseToFile-Postman
* Add the required Test Script code to you collection
* Execute the node.js application e.g. ```node script.js```
* Run your collection using the [Postman Collection Runner](https://learning.getpostman.com/docs/postman/collection-runs/starting-a-collection-run/) 

See the [readme.md](https://github.com/DawMatt/ResponseToFile-Postman/blob/master/README.md) file for further details.

My fork of the original application allows responses to be captured in two forms:

1. Each request is captured in a JSON file named the same as the request
2. All requests are accumulated into a single "_collectionCombined.json" file. Each request is add to a property having the same name as the request

It also allows the captured files to be stored in named subfolders, which is particularly useful when performing multiple executions of a collection with data in test files.
