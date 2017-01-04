# Table of Contents

This section of the OpenTrials documentation is for developers.
Here you can learn about the design of the platform, how to use it and the process for contributing enhancements and bug fixes to the code.

- [Overview](#overview)
- [Database model](data-model.md)
- [API](api.md)

# Overview

OpenTrials project has 4 main components:
  - [Collectors](https://github.com/opentrials/collectors): contains logic for
gathering data (ex: scrapers) and manages the schema for our `warehouse` database
that keeps the data collected from different sources
  - [Processors](https://github.com/opentrials/processors): contains logic for
normalizing and enriching data in our `warehouse` and API `database` and manages our file storage
  - [OpenTrials API](https://github.com/opentrials/api): manages the schema for
our `database` and contains logic for exposing and indexing the data inside it
  - [OpenTrials Explorer](https://github.com/opentrials/opentrials): displays data
from our API and manages the `explorer` database that keeps users and user-related data

You can find a more in depth technical overview and tutorials
[for Collectors here](https://github.com/opentrials/collectors/blob/master/docs/overview.md)
and [for Procesors here](https://github.com/opentrials/processors/blob/master/docs/overview.md).
