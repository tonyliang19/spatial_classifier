# Introduction: Machine Learning for Graphs

[The original link](http://web.stanford.edu/class/cs224w/slides/01-intro.pdf)

## Graphs

Graphs are general language for describing and analyzing entities with relations/ interactions.

Types:

 - Event Graphs
 - Computer Networks (pc - laptop - router - etc..)
 - Disease Pathways (DAXX - ABCB1 - CDKN2A - EGFR - ...)
 - Food Webs (`prey_x` - `predator_y` - ...)
 - Particle Networks 
 - Undergound Netwroks (Subway / Skytrain stations)
 - Social Networks
 - ....

Complex domains have a rich <b> relational structure </b>, which can be represented as relational graph.

Graphs are the new frontier of deep learning, as it connect things.

<b>Networks are complex</b>

- Arbitrary size and complex topological structure (i.e. no spatial locality like grids)

![networks_vs_images](img/net_vs_img.jpg)

- No fixed node ordering or reference point
- Often dynamic and have multimodal features

![graph_nn](img/gnn.jpg)


Map nodes to d-dimensional **embeddings** such that similar nodes in the network are embedded close together.

![node_embedding](img/node_emb.jpg)


<b>Different Types of Tasks</b>
![types_tasks](img/types_tasks.jpg)

- **Node classification**: Predict a property of node
  * Ex: categorize online users/ items
- **Link prediction**: Predict whether there are missing links between two nodes.
  * Ex: Knowledge graph completion
- **Graph classification**: Categorize different graphs
  * Ex: Molecule property prediction
- **Clustering**: Detect if nodes form a community
  * Example: Social circle detection
- **Other tasks**:
  * Graph generation: Drug discovery
  * Graph evolution: Physical simulation


## Example of Node-level ML Tasks


Key idea: "Spatial graph"
 - Nodes: Amino acids in protein sequence
 - Edges: Proximity between amino acids (residues)

![spatial_graph](img/spatial_graph.jpg)


### Example of Edge-level ML Tasks

Recommender Systems

Users interacts with items:
 - Watch movies, buy merchandise, listen to music
 - Nodes: Users and items
 - Edges: User-item interactions

Goal: Recommend items users like

![recommender](img/recommend.jpg)

![graph_recommender](img/graph_rec.jpg)


### Example of Subgraph-level ML Tasks

Road Network as a Graph

- Nodes: Road segments
- Edges: Connectivity between road segments
- Prediction: Time of Arrival (ETA)

![trafic_gnn](img/traffic_gnn.jpg)

### Example of Graph-level ML Tasks

Drug discovery

- Antibiotics are small molecular graphs
 - Nodes: Atoms
 - Edges: Chemical bonds

![antiobiotic_graph](img/antiobiotic.jpg)

## Choice of Graph Representation

![components](img/component_network.jpg)

How to build a graph:

Ask yourself what are <b>nodes</b>, what are <b>edges</b>.

- In some cases, there is a unique, unambiguous representation
- In other cases, the representation is by no means unique
- The way you assign links will determine the nature of the question you can study

Directed vs. Undirected Graphs
![direct_vs_undirect](img/directed_undirected.jpg)
