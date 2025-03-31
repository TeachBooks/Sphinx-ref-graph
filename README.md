# Sphinx Reference Graph

## Introduction

This package contains a Sphinx extension for generating and inserting an interactive graph based on internal references and the table of content. A user can tweak the graph to suit their needs. The graph has clickable nodes that link to pages within the Jupyter book.

## What does it do?

Based on the internal references, the table of content, the directives mentioned below and thre provided extension options, a graph is generated, where each node represent a page within the book and each link between two nodes represents a reference between the corresponding pages.

Each node/page can be assigned a tag. All nodes with the same tag will have the same color and, if three or more nodes have the same tag, an extended convex hull will be drawn around nodes with the same tag.

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

- `ref_graph_temp_file`: `ref_graph.temp` (_default_) or **string**:
  - The name of the (temporary) file used to store the information about nodes, tags and links.
- `ref_graph_html_file`: `ref_graph.html` (_default_) or **string**:
  - The name of the `html` file that will contain the generated graph. This file will be included using an iframe at the required locations.
- `ref_graph_internal_links`: `true` (_default_) or `false`:
  - If `true`, all internal references defined in pages of the book will result in a link in the graph.
  - If `false`, all internal references defined in pages of the book will be ignored, including hidden internal references.
- `ref_graph_toc_links`: `true` (_default_) or `false`:
  - If `true`, all references defined in table of content of the book will result in a link in the graph.
  - If `false`, all references defined in table of content of the book will be ignored, including hidden internal references.
  - For details about defining references in the table of content, see [](sec:graph:code).
- `ref_graph_tag_color`: `{}` (_default_) or **Python dictionary**:
  - The **Python dictionary** must be empty or contain key-value pairs of the form `'tag':'color'`, where `'color'` should be a Javascript recognised color, preferably a hex rgb color.
  - If set to a non-empty dictionary, all nodes with the same tag will be given the provided color and for tags with three or more nodes the extended convex hull will be drawn in the same color.
- `ref_graph_remove_links`: `[]` (_default_) or **Python list**:
  - The **Python list** must contain **Python strings**, where each is of the form `"file1 -> file2"`.
  - In the above, `file1` and `file2` must be the paths to `html` files in the compiled book. The paths are assumed to be relative to the main location of the html files of the compiled book.
  - If not empty, each of the entered links will be removed from the graph.
- `ref_graph_group_nodes`: `false` (_default_) or `true`:
  - If `true`, for each tag an extra node will be added.
  - All other nodes with the same tag will obtain a link to this new node.
  - All links pointing to/from another node with the same tag will be altered to point to/from the new node.
- `ref_graph_collapse_group`: `false` (_default_) or `true`:
  - If `True`, similar to ref_graph_group_nodes.
  - In addition all other nodes with the same tag will be removed from the graph.

(sec:graph:code)=
## Provided code
