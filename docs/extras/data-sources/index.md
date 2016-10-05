# Introduction to the data

OpenTrials is a database of information on clinical trials. The database *threads together* information on trials, collected from a wide range of sources, in a single centralised database, and thereby provides value-add for analysis of the data on clinical trials that has not been possible, or has been inaccessible, with publication practices for clinical trials to date.

Here, we'll give a brief rundown of the data available in OpenTrials, and why it is important.

## Clinical trial registries

Data from clinical trial registries forms the core of the OpenTrials database. These registries have metadata about trials, providing, for example, information on the condition(s) being targeted, the intervention(s) being tested, the number and gender of participants, and so on. We pull in this metadata, look for matches across the registers (multiple "records" talking about the same trial), and build an initial thread of public information about trials from these registriess.

One of the primary registers is [ClinicalTrials.gov](https://clinicaltrials.gov). Have a look around there for an understanding of type of information that we get from registries.

## Pubmed

[Pubmed](http://www.ncbi.nlm.nih.gov/pubmed) provides an API exposing over 26 million citations in the biomedical literature. In OpenTrials, we use PubMed as a way to find academic publications that reference clinical trials. This allows us to provide direct links from a trial page, to academic papers that address that trial in some way (usually either introducing a trial and explaining how it will be carried out, or reporting the results of a completed trial).

## FDA

The [FDA](http://www.fda.gov) provides data related to foods and drugs available on the US market. It is a veritable treasure trove of information, and important aspects of this body of knowledge are usable in OpenTrials.

We take data from the FDA in two different "collectors".

First, we use an FDA API to extract information on drug names. This data is used to help normalise our "interventions" data.

Second, we [scrape Drug Approval Packages](http://opentrials.net/2016/08/10/opentrialsfda-unlocking-the-trove-of-clinical-trial-data-in-drugsfda/) (DAP) data from the FDA. Unfortunately, there is no API for this data, and DAP data tends to be in unsearchable, scanned PDF files. However, they are a very high quality source of information on clinical trials, containing detailed information on the methods and results of trials, and required as part of a drug's marketing authorisation (i.e. for a company to get permission to sell the drug, assuming it meets certain standards). 

Typically the information contained in DAPs is less biased than results of clinical trials which are published in academic journals, so are of interest to OpenTrials and its users. For an interesting analysis of this issue, see this paper by [Erick Turner](http://www.nejm.org/doi/full/10.1056/NEJMsa065779).

## HRA

The Health Research Authority is a UK public body that, amongst its activities, grants ethical approval for health research and clinical trials taking place in the UK. As part of the application process, investigators are asked to submit a Lay Summary, explaining the trial in simple terms. These, along with a small amount of other metadata, are available from the HRA website ([example](http://www.hra.nhs.uk/news/research-summaries/a-study-in-moderate-to-severe-active-crohns-disease/)). OpenTrials has been given API access to this data, allowing us to match these lay summaries to trials, enhancing the accessibility of OpenTrials to users.

## Other sources

Data from two other clinical trial registries ([EU CTR](https://www.clinicaltrialsregister.eu) and [WHO ICTRP](http://www.who.int/ictrp)) is also imported. Additionally, the [Cochrane Schizophrenia Group](http://schizophrenia.cochrane.org/) has kindly given us a dataset which contains expert assessments of the methodological quality of individual trials. We also integrate this data onto individual trial pages where available, further enhancing OpenTrials for interested researchers.

There are seven additional sources of data that we’ve extracted, but can’t display because of licensing issues – we’re working with them to get permission to publish.


## Conclusion

Apart from specific data donations, the current OpenTrials database is made up of publicly available data sources, with the important value-add of matching these different data sources together, and enabling further analysis and insights that stem from this fact.

The core "spine" of data that is sourced from clinical trial registers - metadata about trials - is a foundational aspect of the database, on top of which other types of data sources can be matched. These other types of data sources include references to trials in academic literature, systematic reviews, and trial-related documents such as patient consent forms.

As more and more data gets matched onto the existing OpenTrials database, the value of the database increases significantly.
