# Grid Network Project

## Introduction

[PyGrid](https://github.com/OpenMined/PyGrid) is a peer-to-peer network of data owners and data scientists who can collectively train AI models and compute private statistical analysis using privacy-preserving concepts.

In an approach where nodes have different privacy rules, it is necessary to provide an easy visualization and analysis of the network. The Grid Network and Monitor are components that are part of the PyGrid architecture using the dynamic approach that provide an overview of the components that are connected to the network.

### Components

**[Grid Network](https://github.com/OpenMined/GridNetwork)** - A network router used  by the PyGrid platform  
**[Grid Monitor](https://github.com/OpenMined/GridMonitor)** - An user interface for monitoring a network router for PyGrid Platform

### Overview

To make network monitoring easy, we need that the GridNetwork, which serves as DNS for nodes that connect to the network, to be able to serve the information available on the network. 

Information on the network:

- **Nodes** - The nodes connected to the GridNetwork.
  Grid Nodes carry information such as their id, address, status, connected nodes, datasets and models

- **Datasets** - Datasets available in Grid Nodes.
  The datasets have information from their tags, the node it is in, access level (public or private), privacy (plain-text or SMPC), description and shape.
  
- **Models** - Models hosted in Grid Nodes.
  The models have information about its id, the nodes its is in, access level (public or private), privacy (plain-text or SMPC), description, input and output shape, iterations, learning rate and accuracy.
  
Considering this data, we need to create endpoints for data acquisition so that the grid monitor can generate the visualization and allow the monitoring.

### Endpoints

`/nodes` - Returns basic information for all nodes in the network
```
data: { 
  id: {
    address: <url>,
    status: <online | offline | busy >,
    nodes: [id1, id2, …, idx]
  },
  ...
}
```

|Name   |Type  |Description                                                |
|---    |---   |---                                                        |
|id     |string| The node id                                               |
|status |string| The node status, that can be `online`, `offline` or `busy`|
|nodes  |list  | A list with the IDs of the connected nodes                |

`/nodes/<id>` - Returns detailed information about a node on the network

```
data: { 
  id: <id>
  address: <url>,
  status: <online | offline | busy >,
  nodes: [id1, id2, …, idx],
  datasets: [tag1, tag2, …, tagx] 
  models: [modelId1, modelid2, …, modelIdx]
}
```

|Name     |Type  |Description                                                |
|---      |---   |---                                                        |
|id       |string| The node id                                               |
|status   |string| The node status, that can be `online`, `offline` or `busy`|
|nodes    |list  | A list with the IDs of the connected nodes                |
|datasets |list  | A list with the datasets' tags in the node                |
|models   |list  | A list with the IDs of the models in the node             |


`/datasets` - Returns basic information for all datasets in the network
```
data: [ 
  {
    tags: [tag1, tag2, …, tagx],
    access: <public | private>,
    shape: <tuple> #dimensions,
    description: <description>,
    privacy: <plain-text, smpc>,
    nodes: [nodeid1, nodeid2, nodeid3]
  },
  ...
]
```


|Name       |Type  |Description                                                    |
|---        |---   |---                                                            |
|tags       |list  | A list with the dataset tags                                  |
|description|string| A string containing the dataset description                   |
|access     |string| The level of access, that can be `public`, `private`          |
|shape      |tuple | The shape of the dataset                                      |
|privacy    |list  | The privacy of the dataset, that can be `plain-text` or `smpc`|
|nodes      |list  | A list with the IDs of the connected with this dataset        |

`/models` - Returns basic information for all models in the network
```
data: [ 
  {
    id: <model_id>,
    description: <description>,
    privacy: <plain-text | smpc>,
    input: <shape>,
    output: <shape>,
    access: <public | private>,
    iterations: <int>,
    learning_rate: <float>,
    accuracy: <float>,
    nodes: [nodeid1, nodeid2, nodeid3]
  },
  ...
]
```

|Name         |Type  |Description                                                    |
|---          |---   |---                                                            |
|id           |string| The ID of the model                                           |
|description  |string| A string containing the model description                     |
|access       |string| The level of access, that can be `public`, `private`          |
|input        |tuple | The shape of the the input                                    |
|output       |tuple | The shape of the the output                                   |
|iterations   |int   | Number of iterations                                          |
|learning_rate|float | The learning rate of the model                                |
|accuracy     |float | The model accuracy                                            |
|privacy      |list  | The privacy of the dataset, that can be `plain-text` or `smpc`|
|nodes        |list  | A list with the IDs of the connected with this dataset        |

### Projects

#### GridNetwork
- [Create Grid Network REST API (frond-end)](https://github.com/OpenMined/GridNetwork/issues/1)
- [Create node endpoints](https://github.com/OpenMined/GridNetwork/issues/2)
- [Create datasets endpoints](https://github.com/OpenMined/GridNetwork/issues/3)
- [Create model endpoints](https://github.com/OpenMined/GridNetwork/issues/4)
- [Create Grid Network REST API (back-end)](https://github.com/OpenMined/GridNetwork/issues/5)
