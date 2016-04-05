# OpenTrials user stories

A set of user stories to inform platform development.

## Personas

- *Core Developer*: A developer working on the core OpenTrials platform.
- *Contributing Developer*: A developer from outside the core team who would like to assist with the development of the OpenTrials platform.
- *Product Owner*: A person responsible for the core feature set and functionality of the product.
- *App Administrator*: A person responsible for general administration of the application(s).
- *Visiting User*: A user who visits the application(s) and consumes the data via the user interfaces provided.
- *Contributing User*: A user who visits the application(s) with the goal of adding data and content to the platform.
- *Curating User*: A user who has permissions to curate existing data on the platform, as well as submissions of new data for the platform.

## Stories

### Public UIs

#### A. Exploring the database

1. As a *Visiting User*, I want to be able to use a simple search interface, so I can explore and discover the OpenTrials database.
2. As a *Visiting User*, I want to be able to use an advanced search form that allows me to target search based on key attributes and relational data on trials, so I can explore and discover the OpenTrials database with more accuracy.
3. As a *Visiting User*, I want to be able to browse trials by a given condition or intervention, so I can filter my search experience based on topics of direct interest to me.
4. As a *Product Owner*, I want all search queries made by authenticated users to be saved, so that search queries can be used in other public-facing views, and also later be analysed for potential use in record matching.
  - persist in main database, and read back to warehouse at regular intervals?
5. As a *Visiting User*, I want a view I can access when logged that shows me my search query history, so I can easily reuse and tweak my search strategies.
6. As a *Visiting User*, I want a view where I can see search queries made my other users, and click to make the same query, so I can easily reuse knowledge of other database users in my own data exploration.
7. As a *Visiting User*, I want to see a list of acknowledgments/credits/attributions for every single view of data I am exposed to, so that I can always reference the sources of the data that I am viewing.
8. As a *Visiting User*, I want to see if individual patient records are known to be available for a given trial, so that I can directly visit the relevant portal for that data.
9. As a *Visiting User*, when viewing a single trial, I want to see, where it exists, the multiple records for a trial side by side, so that I can view these for any interesting discrepancies.
10. As a *Visiting User*, when viewing a single trial which has multiple records, I want a clear UI element that tells me if the trial has discrepancies across these records, so I can investigate these further if they exist.
11. As a *Visiting User*, I want a search option to filter by trials with known discrepancies, so I can investigate these trials as a group.
12. As a *Visiting User*, if a single data point in the UI is also one subject to a discrepancy in the data (we choose one record's data to display, and another record conflicts on this data point), I want that to be clearly indicated where the data is displayed, so I know that the data I read is potentially contestable.
13. As  *Visiting User*, I want a clear navigational element in the footer to a "Takedown Request" page, which has a form to submit a takedown request, so that I can flag data that may be breaching copyright or other reasons for take down.
14. As a *Product Owner*, I want a clear but low impact navigational item to view "additional data" on a trial, if such data exists and is not presented on the trial page, so that various data outliers for specific trials can still be accessed by users, even if they do not fit in with the trial page design.
15. As a *Visiting User*, I want a search option to filter trials by publication status, so I can investigate trials based on whether or not results have been published.
16. As a *Visiting User*, I want to see simple dashboard views that present the "state of the data" related to clinical trials as known by the OpenTrials database, so that I can gain a general understanding of the state of clinical trial publication and openness.
  - Report on # of ongoing trials
  - Report on # of completed trials (that have published; that are unpublished)
  - Report on top # conditions tested in trials
  - Report on top # interventions tested in trials
  - Report on top # sponsors of trials
  - Report on top # investigators of trials
  - Report on top # institutes associated with conducting trials
  - Report on institute with most complete but unpublished trials

#### B. Contributing and curating data

1. As *Product Owner*, I want visitors to be able to authenticate with OpenTrials via an OAuth provider, so that the platform can offer features based on user accounts.
2. As a *Product Owner*, I want user accounts to have basic permission levels implemented via *roles*, so that certain users can be authorized to perform certain actions.
  - `standard`: can login and save search history.
  - `curator`: `standard` + allowed various read and write actions to curate the database.
  - `administrator`: `curator` + allowed various read and write actions to manage users.
3. As a *Contributing User*, I want to be able to add data to OpenTrials, related to a given trial, from a given trial page, so I can enrich the data about a trial in the OpenTrials database.
4. As a *Contributing User*, I want to be able to add data to OpenTrials from a generic "add data" page, so I can add data that is not related to any trials I could find in the OpenTrials database.
5. As an *App Administrator*, I want all files and metadata uploaded by *Contributing Users* to be saved to the datastore and the warehouse database, for further manual action by *Curating Users*.
6. As a *Curating User*, I want to be able to see all files that *Contributing Users* have uploaded, so that I can assess steps for action for those files.
7. As a *Curating User*, I want to be able to access a view that allows me to *validate* (yes; no) on a record match made, so I can help improve the quality of he OpenTrials database.
8. As a *Curating User* && *Visiting User*, I want to be able to view all *TrialRecords* by matched/unmatched status, so I can assess the quality of existing record matching processes.
9. As a *Curating User* && *Visiting User*, I want to be able to view all matched *TrialRecords* by *match type* (ID, title, user, etc.), so I can assess the quality of existing record matching processes.
10. As a *Curating User* && *Visiting User*, I want to be able to make matches between existing matched or unmatched records, so that this information can be used in the *Warehouse* to improve data normalisation across various records/entities.
11. As a *Curating User*, I want to be able to view all matches and validations made by *Visiting Users*, so I can further validate this work and it can be used in the *Warehouse* to improve data normalisation across various records/entities.

### Public APIs

#### C. API usage

1. As an *App Administrator*, I want API consumers to use API keys, so I can study and measure API usage patterns.

### Data Warehouse

#### D. Data storage and processing

1. As a *Product Owner*, I want a storage solution for data from a range of publicly accessible clinical trial registers, so the database can be built on this initial set of data about trials.
2. As an *Product Owner*, I want a storage solution for existing meta data on papers published in academic journals, so linkages from this data to the trial meta data in storage can be made.
3. As a *Product Owner*, I want a storage solution for selected text from papers published in academic journals (example: abstracts), so linkages from this data to the trial meta data in storage can be made.
4. As a *Product Owner*, I want a storage solution for regulatory documents associated with clinical trials, so copies of these documents can be cached and/or persisted, as part of the information graph on clinical trials.
5. As a *Product Owner*, I want a storage solution for regulatory document meta data, so information about the source(s) of such meta data can be stored.
6. As a *Product Owner*, I want a storage solution for trial paperwork associated with clinical trials, so copies of these documents can be cached/persisted, as part of the information graph on clinical trials.
7. As a *Product Owner*, I want a storage solution for trial paperwork meta data, so information about the source(s) of such meta data can be stored.
8. As a *Product Owner*, I want record matching based on exact match of trial identifiers (noting there can be multiple trial identifiers for a given trial, and we only need a match on at least one of them), so that clinical trial data and documents can be threaded together to build a (more) complete picture of data on a trial.
9. As a *Product Owner*, I want record matching based on exact match of scientific titles (noting there can be multiple trial identifiers for a given trial, and we only need a match on at least one of them), so we can thread together clinical trial data and documents.
10. As a *Product Owner*, I want all data in the database (each record) to have provenance information stored, so that credit and attribution can be assigned correctly.
11. As a *Product Owner*, I want all data-related actions (example: ingest, transform, export) to have an associated record of the action, so we have a persistent audit trial of the growth and change of the warehouse and public database.
12. As a *Product Owner*, I want basic analytics from core warehouse processes, so I can assess our matching and linking status at any given time.
13. As a *Product Owner*, I want a regular dump of the database to a data package on a file storage system, as a static, publicly accessible dump of the basic data the platform has.
14. As a *Product Owner*, I want a datastore with a directory per ideal trial, so all assets related to a trial are stored in a single location. (example below, not necessarily how it will look)
  - `/{IDEAL_TRIAL_ID}/`
  - `/{IDEAL_TRIAL_ID}/records/{here goes the trial record data}`
  - `/{IDEAL_TRIAL_ID}/documents/{here goes all other trial-related files}`
15. As a *Product Owner*, I want a flat file storage area for data uploaded to the system by users, so that this data can be assessed before it makes its way into the warehouse proper.

