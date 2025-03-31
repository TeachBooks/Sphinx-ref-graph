# Sphinx Reference Graph

## Introduction

This package contains a Sphinx extension for generating and inserting an interactive graph based on internal references and the table of content. A user can tweak the graph to suit their needs. The graph has clickable nodes that link to pages within the Jupyter book.

## What does it do?

Based on the internal references, the table of content, the directives mentioned below and thre provided extension options, a graph is generated, where each node represent a page within the book and each edgebetween two nodes represents a reference between the corresponding pages.

This extension provides several Sphinx directives:

- `refgraph`:
  - This directive inserts the generated graph at the specified location.
- `refgraphtag`:
  - This directive can be used to assign a tag to a page, which will be used in the graph to group nodes together.
- `refgraphhidden`:
  - This directive can be used to include hidden references, to force edges in the graph. 

## Installation

To use this extenstion, follow these steps:

**Step 1: Install the Package**

Install the module `sphinx--ref-graph` package using `pip`:
```
pip install git+https://github.com/TeachBooks/Sphinx-ref-graph.git
```
    
**Step 2: Add to `requirements.txt`**

Make sure that the package is included in your project's `requirements.txt` to track the dependency:
```
git+https://github.com/TeachBooks/Sphinx-ref-graph.git
```

**Step 3: Enable in `_config.yml`**

In your `_config.yml` file, add the extension to the list of Sphinx extra extensions (**important**: underscore, not dash this time):
```
sphinx: 
    extra_extensions:
        .
        .
        .
        - sphinx_ref_graph
        .
        .
        .
```

## Configuration

The extension provides several configuration values, which can be added to `_config.yml`:

```yaml
sphinx: 
    config:
        -
        -
        -
        ref_graph_temp_file:      ref_graph.temp # default value
        ref_graph_html_file:      ref_graph.html # default value
        ref_graph_internal_links: true           # default value
        ref_graph_toc_links:      true           # default value
        ref_graph_tag_color:      {}             # default value
        ref_graph_remove_links:   []             # default value
        ref_graph_group_nodes:    false          # default value
        ref_graph_collapse_group: false          # default value
        -
        -
        -
```

An explination of each configuration value:

