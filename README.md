# opentrials-datamodel

Work towards specifying a data model for the Open Trials project.

## ER-Diagram

![ER-Diagram](https://cloud.githubusercontent.com/assets/557395/9845780/4a1989e6-5ad6-11e5-9e0d-9fb6769638a5.png)

## Description

### Entities

- `Trial` - the main entity, clinical study (16k)
- `Source` - source of data, e.g. "Cochrane" (1)
- `Condition` - illness, injury, impairment etc (256)
- `Method` - trial type, methodology (45)
- `Drug` - a chemical substance to heal people (0)
- `Review` - a publication about a trial (20k)
- `Document` - blob document to associate with any entity (0)

### Relations

Any `Trial` has a `Source` (where we've got the data).

With `Trial` can be associated one or many (m2m relation):
- `Condition`
- `Method`
- `Drug`
- `Review`
- `Document`

With `Review` can be associated one or many (m2m relation):
- `Document`
