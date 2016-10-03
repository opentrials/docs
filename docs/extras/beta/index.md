# OpenTrials beta

Hello fans of evidence-based medicine and open data!

We've recently launched the public beta of OpenTrials, after announcing the start of work on the platform on [February 10th, 2016](http://opentrials.net/2016/02/10/opentrials-technical-roadmap/).

We are very excited about OpenTrials, and its potential role as part of the ecosystem to change the way clinical trials are conducted and reported on.

In this post we'll look at the features that are available in the OpenTrials beta release, and what is in the pipeline on the road to a proper v1 release.

## Features

OpenTrials is designed as a modular platform, employing a set of loosely coupled components that handle distinct tasks from the collection of data from external sources, through to the exposing of data for consumption via the API or a UI.

In the [announcement post](http://opentrials.net/2016/02/10/opentrials-technical-roadmap/) for the platform, we presented two diagrams that describe the architecture of the platform, and the data model that OpenTrials employs. The design presented then has not significantly changed, and you can see those diagrams below for convenience.

<img src="images/architecture.png" width="600" style="text-align: center; display: block; margin: 0 auto;" title="OpenTrials Architecture Overview">

<img src="images/model.png" width="600" style="text-align: center; display: block; margin: 0 auto;" title="OpenTrials Data Model Overview">

What those diagrams do not reveal is the actual feature set exposed to users, so we'll highlight the major features here.

### API

The API is currently at **v1**. The base endpoint for the API is [here](http://api.opentrials.net/v1/), and interactive documentation for the API can be found [here](http://api.opentrials.net/v1/docs/).

The API exposes several RESTful endpoints that allow querying the primary entities of the OpenTrials data model. This is particularly useful for creating applications that pagination through related data, or where the application has identifiers for particular objects and wants to query all information for those objects.

The API also exposes a search endpoint, which is backed by Elasticsearch. This allows for deep queries into the entire database, and does not necessarily require any knowledge of the data model, or the relations between entities, to yield useful results. We've found that, given the nature of the data itself, the search endpoint is the most useful endpoint for regular use.

Our API implements the [Open APIs specification](https://openapis.org). One of the many great benefits of implementing against Open APIs is that client libraries can be auto-generated from the spec itself. So, fire up a REPL in [Python](https://github.com/Yelp/bravado), [JavaScript](https://github.com/swagger-api/swagger-js) or any other language that has a Swagger/Open APIs implementation, and start playing with the data.

### Explorer UI

The [Explorer UI](https://explorer.opentrials.net) is the main portal into the OpenTrials data. It is based on a search-driven user experience, and once a user reach a trial page, further navigation into the related entities for that trial.

The explorer easily enables users to navigate back to the data sources used to populate the database, and notably features many prompts for user contributions to help enhance the database by either identifying errors or contributing new data.

We are very happy with the usability of the Explorer UI, and we hope you will be too.

### Query UI

The [Query UI](https://query.opentrials.net/) is a way to perform ad hoc SQL queries over the entire OpenTrials data warehouse, and then do interesting visualisations with the results of those queries.

We leverage the excellent [Re:dash](http://redash.io) for this, and we've had great success in the lead up to the beta in using this to extract interesting insights out of the data.

### Crowdsourcing UI

The [Crowdsourcing UI](http://crowdcrafting.org/account/opentrials/) is a way to allow users to help us improve the OpenTrials database via an interactive process, either validating data matches that have been made, or by making new manual matches across different records in the database.

We leverage the excellent [Crowdcrafting](https://crowdcrafting.org) for this. At beta, we are launching with a preview of this feature by exposing a "task" to validate matches we've automatically made in processing clinical trial records.

### Other features

There are many "behind the scenes" features related to what we call the "data warehouse". It is especially important to understand these if you plan on contributing code to OpenTrials. The major features to note here are what we call [collectors](https://github.com/opentrials/collectors) and [processors](https://github.com/opentrials/processors).

As the naming suggests, collectors are responsible for bring external data into the database, and processors work on that data for matching, cleaning, normalisation, and the generation of the public API database.

## Data

Of course, the code we are writing is all directed to a single purpose - building a centralised database for information related to clinical trials. To this end, the majority of the work done over the last 6-8 months has been around data collection and processing. Likewise, going forward, this is really the area on which most effort will be focused.

Our focus so far has been on building out the spine of the database using data from clinical trial registers. This data provides the essential information that we need to thread together additional data from a range of other sources.

We've also integrated a data donation related to schizophrenia from [Cochrane](http://www.cochrane.org), systematic review data from the [UK Health Research Authority](http://www.hra.nhs.uk), references to clinical trials in academic literature from [PubMed](https://www.ncbi.nlm.nih.gov/pubmed), and more.

For more information on the data in the OpenTrials database at present, read our [introduction to the data](http://docs.opentrials.net/en/latest/extras/roadmap/).

## Coming up

In terms of the technical platform, we will not be adding many more features. We'll expand the crowd sourcing tasks available, to facilitate user contribution to the database, and we will open up some more specific API endpoints. Of course, there are always bugs and small enhancements to work on.

Most of the work remaining is closely tied to the data. In terms of data cleaning, entity normalisation, and record matching, we've barely touched the surface. We'll be particularly focused on this over the next 6 months, and this is a great area to contribute if you have some data wrangling and data science interest or expertise.

We'll also integrate a few more data sources. These are sources we've been working on over the last months, but are not yet at a stage to expose over the public API. Of note here are an integration with [Epistemonikos](http://www.epistemonikos.org), which is a rich source of quality systematic reviews, and [OpenAIRE](https://www.openaire.eu), which has an impressive text and data mining feature set that is helping us uncover more clinical trial references in academic publications.

## Contributing

As with all Open Knowledge International projects, we welcome and encourage contribution. For the technical work on OpenTrials, contributions can mean any or all of code, documentation, testing, etc. See [OpenTrials on GitHub](https://github.com/opentrials) for all the repositories with interesting tasks to take up. Also, you can contact [opentrials@okfn.org](mailto:opentrials@okfn.org) if you would like to contribute!
