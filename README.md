# facct_2022_dataset
The dataset for our FAccT 2022 Paper "Equitable Public Bus Network Optimization for Social Good: A Case Study of Singapore" is available on the following google drive [link](https://drive.google.com/drive/folders/1LTFuZdID8b5nL_00kWbgEgdnWoeObEJe)

Please cite our paper if using our dataset:

```
@inproceedings{Tedjopurnomo2022,
    title={Equitable Public Bus Network Optimization for Social Good: A Case Study of Singapore},
    author={Tedjopurnomo, David and Bao, Zhifeng and Choudhury, Farhana and Luo, Hui and Qin, A. K.},
    year = {2022},
    booktitle = {Proceedings of the 2022 ACM Conference on Fairness, Accountability, and Transparency},
    series = {FAccT '22}
}
```

There are nine pickle (.pkl) files in this repository, the details of which are given below

## all_areas.pkl
<details>

<summary>Click to expand</summary>
This file contains the data of Singapore's planning areas. There are 55 Singapore planning areas, however, as 5 of them do not have any bus stops data, we only record the data of 50 planning areas. This is a nested dictionary. To access the level-two dictionary containing data of one area, query the dictionary by providing the area name `String` as the key in uppercase (e.g. "PASIR RIS")

The inner dictionary contains the following key-value pairs:


| Key| Value |
| --- | --- |
| `Shape` | `String` that says `Polygon` (Unused) |
| `Planning Area Name` | `String` of the area name; same as the level-one dictionary key |
| `Planning Area Code` | `String` for the shorthand code of area name |
| `Central Area Indicator` | `String` that indicates the central area this planning area is in   |
| `Region Name` | `String` that shows in which of Singapore's five regions this area is located in  |
| `Region Code` | `String` shorthand code for the `Region Name` |
| `INC_CRC` | `String` possibly denoting unique code for the area (Unused) |
| `FMEL_UPD_D` | `String` original upload date of the data (Unused) |
| `X_ADDR` | `String` possibly storing the x-axis location of the area (Unused) |
| `Y_ADDR` | `String` possibly storing the y-axis location of the area (Unused) |
| `SHAPE_Length` | `String` denoting the length of the area (Unused) |
| `SHAPE_Area` | `String` denoting the size of the area in kilometers  |
| `Boundaries` | `shapely.geometry.polygon.Polygon` containing the area's boundaries |
| `Bus Stops` | `List` containing this area's bus stops, each denoted with a `String` ID |
| `Race` | `List` containing `tuples` of `String` and `integer` for the race name and population count of that race respectively |
| `Sex` | `List` containing `tuples` of `String` and `integer` for the sex name and population count of that sex respectively |
| `Qualification` | `List` containing `tuples` of `String` and `integer` for the qualification name and population count of that qualification respectively |
| `Income` | `List` containing `tuples` of `List` and `integer` for the income ranges and population count within that income range respectively |
| `Stop to Area` | A two-level nested `dict` containing the stop-to-area efficiency data. The key to the first level dictionary is the `String` of the stop ID within the area and the key to the second level is the `String` of the area name |
| `Stop to Stop` | A two-level nested `dict` containing the stop-to-stop efficiency data. The key to the first level dictionary is the `String` of the stop ID within the area and the key to the second level is the `String` of another stop ID |
| `Car Distance` | A two-level nested `dict` containing the car distance data. The key to the first level dictionary is the `String` of the stop ID within the area and the key to the second level is the `String` of another stop ID, The unit is in meters. |
| `Bus Distance` | A two-level nested `dict` containing the bus distance data, which includes the waiting distance and transfer penalty. The key to the first level dictionary is the `String` of the stop ID within the area and the key to the second level is the `String` of another stop ID, The unit is in meters. |
| `Stop Coverage` | `dict` with a `String` as a key and a `float` as the value. The key denotes a bus stop ID and the float denotes the coverage area of that bus stop. Specifically, each bus stop is assigned a non-overlapping 400 square meters radius for its coverage. The float here stores a bus stop's fraction of area coverage over all bus stop's coverage in that area. For instance, if an area has two bus stops with non-overlapping area total of 800 square meters, each bus stop will have a fraction of 0.5 |
| `Area to Area` | `dict` with a `String` as a key and `Decimal` as the value. The key denotes another area's name and the value denotes this area's efficiency to that area  |
| `Disadvantaged` | `dict` with a `String` as a key and `bool` as the value. The key denotes a demographic factor and the value denotes if this area is a disadvantaged area for that demographic factor |
| `Disadvantaged Percentage` | `dict` with a `String` as a key and `float` as the value. The key denotes a demographic factor and the float denotes the fraction of disadvantaged population for that demographic factor |
| `Average Connectivity` | `Decimal` denoting this area's overall connectivity/efficiency |
</details>

## all_nodes.pkl
<details>

<summary>Click to expand</summary>
This file contains the data of the nodes of Singapore's car graph.  This is a nested dictionary. To access the level-two dictionary containing data of one node, query the dictionary by providing the node ID `String`. There are two types of nodes: bus stops and road junctions. Bus stop IDs are shorter with about 4-5 characters while road junction IDs are longer with about 9-10 characters. 

The inner dictionary contains the following key-value pairs:
| Key| Value |
| --- | --- |
| `ID` | `String` of the node ID, same as the level-one dictionary key |
| `coordinates` | `tuple` of `floats` for the latitude and longitude coordinates of the node |

</details>

## all_edges.pkl
<details>

<summary>Click to expand</summary>
This file contains the data of the edges of Singapore's car graph.  This is a nested dictionary. To access the level-two dictionary containing data of one edge, query the dictionary by providing the edge ID `String`.  

The edges have underscore components which denotes the original edge that has been split on the bus stop contained in that edge.  For instance, edges `39449_1` and `39449_2` are splits of the original edge `39449`, where the split is done on bus stop `96449`.  The original edge `39449` starts on junction with ID `5060088362` and ends on junction with ID `2327165732`.  After the split, edge `39449_1` starts on junction with ID `5060088362` and ends on bus stop `96449`, while edge `39449_2` starts on bus stop `96449` and ends on junction with ID `2327165732`

The inner dictionary contains the following key-value pairs:
| Key| Value |
| --- | --- |
| `Bus Stops` | An empty `list` (Unused) |
| `Coordinates` | `list` of `tuples` of `floats` containing the latitude-longitude pair that constitutes the edge |
| `ID` | `String` of the edge ID, same as the level-one dictionary key |
| `Length` | `float`  for the length of the edge in meters |
| `u` | `String` of node ID which is the origin of the edge. The node ID is the same as in all_nodes.pkl |
| `v` | `String` of node ID which is the destination of the edge. The node ID is the same as in all_nodes.pkl |

</details>

## all_stop_mapmatched.pkl
<details>

<summary>Click to expand</summary>
This file contains the data of Singapore's bus stops after the mapmatching process.  This is a nested dictionary. To access the level-two dictionary containing data of one stop, query the dictionary by providing the bus stop ID `String`. 

The inner dictionary contains the following key-value pairs:
| Key| Value |
| --- | --- |
| `Linestring Old` | `String` containing the linestring of the old (before mapmatching) coordinates |
| `Name` | `String` of the bus stop name |
| `Edge ID` | `String` of the edge ID the bus stop is on. This ID represents the original (i.e. pre-split) edge ID. Refer to the documentation for all_edges.pkl above for details |
| `Road Name` | `String` of the road name the bus stop is on. This refers to the `Edge ID` above |
| `Coordinates Old` | `tuple` of `floats` of latitude-longitude pairs where the bus stop is located. This is before the mapmatching process |
| `Coordinates New` | `tuple` of `floats` of latitude-longitude pairs where the bus stop is located. This is after the mapmatching process |
| `Valid Start` | `bool` denoting whether or not this is a terminal bus stop. In Singapore's case, it is whether or not this bus stop is the start or ending point of at least one bus route |

</details>

## bus_routes.pkl
<details>

<summary>Click to expand</summary>
This file contains the data of Singapore's bus routes.  This is a nested dictionary. To access the level-two dictionary containing data of one route, query the dictionary by providing the bus route ID `String`. 

The inner dictionary contains the following key-value pairs:
| Key| Value |
| --- | --- |
| `seq_no` | `list` of `int` starting from 1 to the number of bus stops in the route (Unused) |
| `stop_id` | `list` of `Strings` representing the bus stop IDs of the bus route |
| `dist` | `list` of `Decimals` representing the distance from the n-th bus stop in the route to the start of the route |
| `wd_first` | `String` representing the bus route's operation start time in the `HHMM` 24-hour format without any leading zero for the hour |
| `wd_last` | `String` representing the bus route's operation end time in the `HHMM` 24-hour format without any leading zero for the hour |
| `frequency` | `list` of `tuples` where each tuple contains two `datetime.time` objects and a float. The two `datetime.time` objects denote a time period and the float denotes the bus frequency/waiting time for that period |
| `startend` | `list` of two `datetime.time` objects containing the bus route's operation start and end time |
| `route_type` | `String` denoting the type of the route. For the Singapore data, the only value will be `bus` |

</details>


## bus_dists.pkl and car_dists.pkl

These files contain the data of Singapore's bus and car distances in meters.  This is a nested dictionary where the key for the first and second level dictionary are both bus stop ID `Strings`. The value is the bus or car distance in meters between the first-level and second-level key's bus stop IDs. This is the same as the one in all_areas.pkl, except in that file, you can only view the bus or car distance from the bus stops in a particular area whereas bus_dists.pkl allows you to access all the distances directly.

## bus_graph.pkl and car_graph.pkl

These files contain `igraph.Graph` objects for the bus and car graph. Refer to the [pyhon igraph documentation](https://igraph.org/python/doc/api/igraph.Graph.html) on how to use this graph. 


