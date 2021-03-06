# Kibana Packages

DynamiteNSM ships with a simple package manager for installing and uninstalling groups Kibana objects.

Packages typically contain searches, visualizations and dashboards combined to facilitate one or more investigatory workflows.

By default, DynamiteNSM will install the `BaseViews` package, which provides a unique blend of host centric and event/alert centric views.

> ⓘ To use the `kibana package` command you must install `dynamite-nsm`.

## Available Packages

| Package Name          | Description                                                                                                                                                                                                    | Author             | Downloads                                                                                                                                                           |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BaseViews | Dashboards are organized around three primary data-models: alerts, conversations, and hosts. This package takes advantage of the shared identifiers embedded in generated models to facilitate deep-dives and pivots. | Dynamite Analytics | [0.3](https://github.com/DynamiteAI/kibana_packages/raw/ceab4764d612cb7693aa243cf0fa19c90f9f7697/BaseViews/dist/BaseViews.tar.gz) [0.4](https://github.com/DynamiteAI/kibana_packages/raw/c5e0818a67995579812ecb94363eb32d301cdb54/BaseViews/dist/BaseViews.tar.gz) |


# Create a Kibana Package


## Package Format Guidelines
We've developed a few internal guidelines that must be followed for those wishing to submit their own package to the Dynamite package repository.
They are available [here](https://github.com/DynamiteAI/kibana_packages/blob/main/package_guidelines.md).

## Setting up a Working Environment

Before you can create a new Kibana package you will need to [setup a working monitor and agent instance](/guides/01_quick_start).
Once the agent starts sending events Kibana's discovery view will quickly fill up, and you can begin creating new visualisations and dashboards.

![](.img/kibana_discovery.png)

The `dynamite-investigator` package provides some out-of-the-box saved searches, useful for filtering and
differentiating between event types. These searches can serve as a basis for creating your own visualizations and dashboards.

![](.img/saved_search_select.png)

## Creating a Visualization
Kibana provides a fairly exhaustive set of visualizations for representing both simple and complex relationships in your data.

You can create a new visualization by double-clicking the `Vizualize` tab in the left-hand sidebar. From there simply select the `Create visualization` button
to enter into the `New Vizualization` interface.

![](.img/new_vizualization.png)

## Adding a Visualization to a Dashboard

Dashboards serve as space to present a variety of visualizations that typically share some common theme.
Kibana dashboards provide the ability to enforce certain global constraints against all visualizations within that dashboard.

For example, the `time-range filter` and any `term filters` or `KQL searches` can be applied consistently accross all visualizations within
a dashboard.

To create a new `Dashboard` double-click the `Dashboard` tab in left-hand sidebar. You may then add any vizualization or saved_search you have created.

![](.img/create_new_dashboard_viz.png)

## Exporting Saved Objects

To export saved objects simply navigate to `Stack Management` in the left-hand sidebar. From there select `Saved Objects` link.
Within this UI you can export all the objects or just those of a certain type.

We suggest that objects are exported for each type and without including related objects. By doing so other developers can easily build
upon the parts of your package most useful to them. 

![](.img/export_saved_object_type.png)

## Creating the Package

Every `kibana package` consists of one or more saved_object.ndjson files and a `manifest.json` file.

The `.ndjson` files are the output of a Kibana export operation as outlined above. A `manifest.json` simply contains
some additional metadata as well as a list of files to be installed via Kibana's saved_object's API.

### manifest.json

```json5
{
	"name": "Baselines",
	"author": "John Doe",
	"author_email": "jdoe@example.com",
	"description": "Includes several base-lining techniques useful for identifying anomalies on small networks",
	"package_type": "saved_objects",
	"file_list": ["config.ndjson", "index_patterns.ndjson", "searches.ndjson", "visualizations.ndjson", "dashboards.ndjson"]

}
```
> **Important!**: The order of appearance in the file_list is important, dependencies should precede their dependants.  

> In the example above `searches.ndjson` relies on or references the data from `index_patterns.ndjson` to be available at installation time, otherwise errors and unexpected behavior may arise.

## Create an Archive

```bash
tar -cvf baselines.tar.gz baselines/*
```
