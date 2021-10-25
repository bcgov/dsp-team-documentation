[![img](https://img.shields.io/badge/Lifecycle-Maturing-007EC6)](https://github.com/bcgov/repomountie/blob/master/doc/lifecycle-badges.md)

# R Projects

## Workflow

- RStudio projects
- [targets](https://books.ropensci.org/targets)
- [arrow](https://arrow.apache.org/docs/r/)

### Best practices when setting up a targets/arrow project:

- targets that are paths should include the `format = 'file'` argument. This enables [reproducibly tracking a file](https://books.ropensci.org/targets/files.html#external-input-files)
- targets should return data not pointers to data. So in practice, this means don't return the R6 object from `open_dataset` but rather `collect` the data inside a function and return actual data

## Visualization

- ggplot2
- tmap
- mapview


## Data Management
- where possible, data should be accessed programmatically using http APIs. An example of this is the [bcdata](https://bcgov.github.io/bcdata/) package


