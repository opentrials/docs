## Table of Contents

  - [Flow of data in OpenTrials](#flow-of-data-in-opentrials)
  - [API database](#api-database)
  - [Warehouse database](#warehouse-database)

## Flow of data in OpenTrials

1. Data about trials, publications etc. is gathered from different registries in 
[Collectors](https://github.com/opentrials/collectors).
2. Most registries have a corresponding table in our `warehouse` database that
follows their data structure. The data gathered from each registry is inserted
into that corresponding table after very little processing (e.g. type conversion, splitting).
3. Data from the `warehouse` is normalized in [Processors](https://github.com/opentrials/processors)
to comply with the structure
of our [API](https://github.com/opentrials/api) `database`. This process involves:
    * separating the data into different entities (`trial`, `publication`, etc.)
    * extracting relevant information from unstructured data (through parsing or
    optical character recognition)
    * matching with existing data based on common identifiers (e.g. NCT ID) to avoid duplication
    * linking related data (e.g. a `publication` with its `trial`)
4. Normalized data is introduced into our API `database`.
5. Our API indexes the data to make it easily searchable.
6. Data is ready to be searched and visualized through the API or 
[OpenTrials Explorer](https://github.com/opentrials/opentrials).


## API database

The [OpenTrials API documentation on endpoints](https://api.opentrials.net/v1/docs/) includes a
detailed and up-to-date description of each table and its relations, with description
and type for each field.
Just follow the route of the model you're interested in, expand it and press `Model`
next to `Example Value` (where the cursor points in the image below):

![Trial model description in Swagger](https://github.com/opentrials/docs/blob/master/docs/assets/images/trial_model_swagger.png?raw=true)

What each table/entity represents:

- `Source` - data registries and other sources of data (e.g. clinicaltrials.gov)
- `Trial` - the main entity, represents a clinical study
- `Record` - also represents a clinical study; more on its role in section [Discrepancies](#discrepancies)
- `Condition` - illness, injury, impairment
- `Intervention` - treatment, therapy, drug
- `Organization` - institutions, companies involved in a trial
- `Persons` - people involved in a trial
- `Locations` - geographical scope of a trial; city, country, region
- `RiskOfBias` - the risk of bias in a given trial as evaluated in a systematic review
(e.g. [Cochrane Library](http://www.cochranelibrary.com/) review)
- `RiskOfBiasCriteria` - criteria for determining the risk of bias
- `FDAApplication` - application for an [FDA](http://www.fda.gov/) aprroval
- `FDAApproval` - the approval of an [FDA](http://www.fda.gov/) application  
- `Document` - generic entity that keeps metadata about different documents associated
with other entities (e.g. FDA approval letter)
- `File` - generic entity that keeps metadata about files in our file storage

#### Discrepancies

We collect `trials` from multiple sources. Some `trials` appear in multiple
registries and each registry gives certain information about them, more or less updated and verified.
To work with these variations, we keep a version of the `trial` from each registry as a `record`.

Sometimes these versions can have contradictory information.
For example one `record` could say the `trial` was completed while another that it's ongoing.
These contradictory pieces of information are what we call *discrepancies*.

To maximize the accuracy of information in `trials`, we have a system to prioritize
from which `records` to take it. For example, if a `trial` has a `record` from a registry that verifies its
information and a `record` from a registry that doesn't, we will assign to the `trial` the values from the former.
This makes the first `record` the *primary* source of data for the `trial`.

## Warehouse database

As the name suggests, the purpose of `warehouse` is to keep collected data in a very raw form.
Its structure is very simple: we have several tables that correspond to different data
registries (e.g. `euctr`, `pubmed`). These tables are not connected to each other and they
have a flat schema that follows the structure of data in the registries they correspond to.
