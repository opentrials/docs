# OpenTrials project ideas

OpenTrials is really a platform on which other things can be built, and has been designed as such from day one.

This means that not only are there many ways to contribute to the core platform development, but also it is invited and encouraged to leverage the code and data for custom projects!

See the [Technical Roadmap](http://docs.opentrials.net/en/latest/extras/roadmap/) and the [beta announcement](http://docs.opentrials.net/en/latest/extras/beta/)for some more specific details on the platform, what has been built, and what is in our pipeline.

Here, we'll discuss some specific project ideas that could be taken up at a hack day, for a weekend project, or even for a longer period as a contribution to the OpenTrials ecosystem.

## Ideas

### Normalise organisation data

#### What

The OpenTrials data warehouse collects data from various sources, and as part of the cleaning process, does an initial extraction of various entities in the data. One such entity is "organisations". Our table holds organisation data (companies, research centres, universities etc) that has been extracted from the clinical trial metadata in the OpenTrials database.

This data in and of itself is interesting, presenting a view into which organisations are funding and conducting clinical trials. In order to make this data more effective, it needs to be cleaned up and normalised.

#### How

Use [OpenCorporates](https://opencorporates.com) to get canonical information on companies, or perhaps look for other sources that are specifically targeted to [Pharmaceutical companies](https://en.wikipedia.org/wiki/List_of_pharmaceutical_companies) or [universities](https://en.wikipedia.org/wiki/Category:Medical_research_institutes_in_the_United_States). Use such sources as a clean lookup table, and identify matches between these and data in the OpenTrials database.

Use fuzzy matching on names, or other techniques. Create a [processor](https://github.com/opentrials/processors) that encapsulates your normalisation routines and submit a [pull request](https://github.com/opentrials/processors/pulls) for peer review.

#### Skills

- Intermediate data wrangling
- Intermediate Python
- Knowledge of existing dictionaries/lookup services to clean and normalise data against

### Normalise person data

#### What

As with the above idea on organisation data, similar opportunities exist for normalising person data in the OpenTrials database. This data has been extracted into a dedicated table for the Person entity, but needs much cleaning and normalisation in order to turn it into a usable resource.

#### How

As lookup tables for persons are harder to come by than for organisations, the suggested approach would be to do fuzzy matching across the names as a first step to creating a normalised dataset.

Beyond this important step, one could then use the cleaned list of names against a generic search engine, and look for matches with a high degree of alignment to the medical domain, and start to extract additional data on these persons, such as academic publications, association with research departments etc. Additionally, for trials with [linked publications](http://explorer.opentrials.net/search?q=&has_publications=true), names matches could be looked up against the list of authors for publications known to relate to the trial (NB. multiple publications may relate to a particular trial).

Building such a body of knowledge, this could then be triangulated with the rest of the OpenTrials database, identifying new academic publications related to trials, for example.

#### Skills

- Advanced data wrangling
- Intermediate Python

### Collect new data sources

#### What

In OpenTrials, we have [collectors](https://github.com/opentrials/collectors), which use modules and functions of Python code to get data from some external source into the OpenTrials warehouse database for further processing.

There are many data sources available. So far we've build out the spine of the database with core clinical trial records, but there are tens of additional sources that can potentially be matched onto the clinical trials we know about, and provide value to the database.

#### How

See the [documentation for all existing collectors](https://github.com/opentrials/collectors/tree/master/docs/collectors) and start your own with a new data source! A good place to begin would be to see if any collectors have not yet been written for the 15 [WHO Primary Registries](http://www.who.int/ictrp/network/primary/en/).

#### Skills

- Intermediate Python
- Some basic domain knowledge (to identify additional sources to collect and persist in the OpenTrials warehouse)

### Probabilistic record matching for trial data

#### What

The OpenTrials database threads trial information together from a range of disparate sources. This is currently done via exact matching using unique trial identifiers. Due to the lack of universal standards for identifiers, the presence of multiple identifier types, and the fact that not all records even have an identifier, it is not possible to make all links with exact matching.

Probabilistic matching will allow us to build up a knowledge base of likely matches across trials based on similarities on key data fields.

#### How

Write one or many [processors](https://github.com/opentrials/processors) that do matching across all trial records using probabilistic techniques.

#### Skills

- Advanced data science/wrangling
- Intermediate Python

### Basic outlier detection

#### What

There is much that can potentially be learned just by looking for outliers in a large dataset. Even without specific domain knowledge, building a set of queries to find outliers can be a first step in asking questions about the data. As a starting point, consider such possibilities around participation, location, age range or interventions for a particular condition.

#### How

Using the [OpenTrials query interface](https://query.opentrials.net/), build a set of queries designed for outlier detection across key data fields.

- [A simple introduction to outlier detection with SQL](https://www.periscopedata.com/blog/outlier-detection-in-sql.html)

#### Skills

- Intermediate SQL

### Visualisation of discrepancies

#### What

By collecting a significant amount of publicly available data on clinical trials, we've found that different records for the same trial often have different information. Such differences can be, for example, in the supposed number of participants who took part in a trial, whether the trial is still ongoing, or if the trial's results have been published.

These discrepancies are important as all these public sources of trial data can be taken as "official", and referenced in the academic literature, for example. Therefore, exposing information on discrepancies is an important outcome of building the OpenTrials database.

#### How

Use the [OpenTrials API](http://api.opentrials.net/v1/docs/) to find trials with detected discrepancies. Look for common types of discrepancies, and build basic visualisations based on type (e.g.: the publication date or participation count) or frequency (e.g. are discrepancies becoming more common or less common?).

#### Skills

- Intermediate JavaScript and HTML
- Basic knowledge of visualisations

### Visualise the relationship between conditions and unpublished/published/ongoing trials

#### What

Certain conditions can be subject to clinical trials at different frequencies over time. Of course, there can be very good reasons for this, for example, a boost in clinical trials for Ebola around the Ebola crisis of 2014. Choose one or several conditions, and show information on a timeline for ongoing trials, trials that have finished and have published results, and trials that have finished yet do not have published results.

#### How

Use the [OpenTrials API](http://api.opentrials.net/v1/docs/) to find trials information on trials related to certain conditions.

#### Skills

- Intermediate JavaScript and HTML
- Basic knowledge of visualisations

### OpenTrials UI/X

#### What

The main user interface for OpenTrials is the [Explorer](https://explorer.opentrials.net). It presents a simple, search-based UI for discovering what is in the OpenTrials database. Experiment with alternate ways of displaying information, or, for submitting information to OpenTrials.

#### How

With whatever web design tools you are fluent in!

#### Skills

- Intermediate UI and UX
- Basic HTML, CSS and Javascript

### Some general solutions of use to domain experts

- For all trials registered in two or more places, show the prespecified primary and secondary outcomes (side by side?), so that discrepancies can be found
- Search for all trials in a given geographical area, that are recruiting participants for a given condition, age, and gender (e.g. cancer trials in London for men).

## Resources

- [API docs](https://api.opentrials.net/v1/docs/)
- [General developer and contributor docs](https://api.opentrials.net/v1/docs/)
- [SQL query interface](https://query.opentrials.net/)
- [Explorer UI](https://explorer.opentrials.net/)
- [The academic paper introducing OpenTrials](https://trialsjournal.biomedcentral.com/articles/10.1186/s13063-016-1290-8)
- [A blog post by Ben Goldacre on the What, Why and How of OpenTrials](http://blogs.biomedcentral.com/on-medicine/2016/04/14/opentrials-what-why-and-how/)
