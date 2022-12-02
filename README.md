# Live-Graph-Lab
This is the source code for our experiments.

## Requirements
* python3.8
* pytorch==1.11.0
* torch-scatter==2.0.9
* torch-sparse==0.6.13
* torch-cluster==1.6.0
* torch-geometric==2.0.4
* networkx==2.8.6
* numpy==1.21.5
* matplotlib==3.5.3
* pandas==1.4.2
* scipy==1.9.1
* snap

## Datasets 
We extract all the blocks before Aug 1st, 2022 (i.e., from block #0 to block #15,255,104). Then, we parse all the transaction data and log data via toolkit Ethereum ETL. Through this way, we obtain a network with more than 4.5 million nodes and 124 million edges. The data are stored in a tabular format with the following headers: `collection address`, `block number`, `from address`, `to address`, `token id`, `transaction hash`, `value` and `timestamp`. The processed dataset is available at [here](https://nusu-my.sharepoint.com/:u:/g/personal/e0261911_u_nus_edu/EdglBhR7F3JAkRM9HtOQXkoBw6qJM8NyW8n6Bgm6jT2_YQ).

## Analysis
All the codes for graph analysis are included in folder `./analysis`. Just execuate each python file to generate the figures. For example, you can reproduce Figure 1 and Figure 2 by running `local-graph-properties.py` and `global-graph-properties.py`, respectively.


## Temporal Link Prediction
For link prediction task, we remove all the transactions associated with the `Null` address, which results in 3.13 million nodes and 23.13 million edges in the directed graph. The data file includes four columns: `from id`, `to id`, `edge weight` and `timestamp`. The processed dataset is available at [here](https://drive.google.com/file/d/1m5nsPbFlxVOU3GMb4TX69sfweLrSCyzD/view?usp=share_link).

For detailed experiment settings, please refer to `README.md` in `./link-prediction`.


## Continuous Subgraph Matching
Similar to link prediction task, we also remove all the transactions associated with the `Null` address. We use NFT transactions from year 2017 to the end of 2021 as the initial graph, and then the transactions in the year of 2022 are regarded as the insertion streams. Since the original nodes and edges are unlabeled, we randomly assign one of 30 labels to each node, and we do not assign labels for edges and we use the edges' directions as labels. The data are structured as follows:

### Query Graph
Each line in the query graph file represent a vertex or an edge.

* A vertex is represented by `v <vertex-id> <vertex-label>`.
* An edge is represented by e `<vertex-id-1> <vertex-id-2> <edge-label>`.

The two endpoints of an edge must appear before the edge. For example,
```
v 0 0
v 1 0
e 0 1 0
v 2 1
e 0 2 1
e 2 1 2
```

### Initial Data Graph
The initial data graph file has the same format as the query graph file.

### Graph Update Stream
Graph update stream is a collection of insertions and deletions of a vertex or an edge.

* A vertex insertion is represented by `v <vertex-id> <vertex-label>`.
* A vertex deletion is represented by `-v <vertex-id> <vertex-label>`.
* An edge insertion is represented by `e <vertex-id-1> <vertex-id-2> <edge-label>`.
* An edge deletion is represented by `-e <vertex-id-1> <vertex-id-2> <edge-label>`.

The vertex or edge to be deleted must exist in the graph, and the label must be the same as that in the graph. If an edge is inserted to the data graph, both its endpoints must exist. For example,
```
v 3 1
e 2 3 2
-v 2 1
-e 0 1 0
```
The graph datasets and their corresponding querysets used in our paper can be downloaded [here](https://drive.google.com/drive/folders/1Fuceh_P_d3vh1_-XCIYKTsu2j9vIZeSm?usp=share_link).

For detailed experiment settings, please refer to `README.md` in `./csm`.

