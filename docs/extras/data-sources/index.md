# Introduction to the data

OpenTrials is a database of information on clinical trials. The database *threads together* information on trials, collected from a wide range of sources, in a single centralised database, and thereby provides value-add for analysis of the data on clinical trials that has not been possible, or has been inaccessible, with publication practices for clinical trials to date.

Here, we'll give a brief rundown of the data available in OpenTrials, and why it is important.

## Clinical trial registers

Data from clinical trial registers forms the core of the OpenTrials database. These registers have metadata about trials, providing, for example, information on the interventions on trial, the number and gender of participants, and so on. We pull in this metadata, look for matches across the registers (multiple "records" talking about the same trial), and build an initial thread of public information about trials from these registers.

One of the primary registers is [ClinicalTrials.gov](https://clinicaltrials.gov). Have a look around there for an understanding of type of information that we get from registers.

## Pubmed

[Pubmed](http://www.ncbi.nlm.nih.gov/pubmed) provides an API exposing over 26 million citations in biomedical literature. In OpenTrials, we use PubMed as a way to find academic publications that reference clinical trials. This allows us to provide direct links from a trial page, to academic papers that address that trial in some way.

## FDA

The [FDA](http://www.fda.gov) provides data related to foods and drugs available on the US market. It is a veritable treasure trove of information, and important aspects of this body of knowledge are usable in OpenTrials.

We take data from the FDA in two different "collectors".

First, we use an FDA API to extract information on drug names. This data is used to help normalise our "interventions" data.

Second, we scrape Drug Approval Package (DAP) data from the FDA. Unfortunately, there is no API for this data, and yet it provides a very high quality source of information on clinical trials, by way of information on drugs that slated to reach the market.

## HRA

@benmeg I don't understand this data source well enough. Please full out.

## Other sources

@benmeg you'll have to fill out more information here.

## Conclusion

Apart from specific data donations, the current OpenTrials database is made up of publicly available data sources, with the important value-add of matching these different data sources together, and enabling further analysis and insights that stem from this fact.

The core "spine" of data that is sourced from clinical trial registers - metadata about trials - is a foundational aspect of the database, on top of which other types of data sources can be matched. These other types of data sources include references to trials in academic literature, systematic reviews, and trial-related documents such as patient consent forms.

As more and more data gets matched onto the existing OpenTrials database, the value of the database increases significantly.
