# Cluster Analysis using Python and Open Street Maps

To Identify Commercial Centers in a City using DBSCAN Clustering Technique

## Getting Started

Clone the repo and go through the notebook for further details

### Prerequisites

Prerequisites
```
Jupyter Notebook
numpy
pandas
matplotlib
scikit-learn
geopy
utm
```
To install, just do this.
```
pip install -r requirements.txt
```

### Information

OpenStreetMap is a collaborative project to create a free editable map of the world. It is defined on the basis of three elements, the node, the way and the relation.
Nodes can be used on their own to define point features. 
It consists of a single point in space defined by its latitude, longitude and node id.
Many of the elements come with tags which describe specific features represented as key-value pairs.
A way on the other hand is a ordered list of nodes, which could correspond to a street or the outline of a house.
The final data element is a relation which is also an ordered list containing either nodes, ways or even other relations.
Overpass API works by writing queries.
#### Query
```
(
nwr["shop"](27.0,76.2419,28.6514,77.2519);
nwr["amenity"](27.0,76.2419,28.6514,77.2519);
);
/*added by auto repair*/
(._;>;);
/*end of auto repair*/
out;
```
nwr checks for nodes, ways or relations that lie within the bounding box specified by the bounding box. I chose the presence of shops and amenities as a metric for detecting if a place was an important commercial center. An important commercial centre,say like a mall, should have a large number of nodes per unit area
To detect  whether a given area is a commercial centre is a clustering problem and based on (this,)[https://triphappy.com/blog/finding-the-best-places-to-stay-anywhere/15]
DBSCAN is the best suited one for the purpose.
DBSCAN is a density based clustering algorithm that divides a dataset into subgroups of high density regions. There are two parameters required for DBSCAN: epsilon (ε) and minimum amount of points required to form a cluster (minPts).

ε is a distance parameter that defines the radius to search for nearby neighbors. We can imagine each data point having a circle with radius ε drawn around it. Using ε and minPts, we can classify each data point as:

Core point – a point that has at least a minimum number of other points (minPts) within its ε radius.
Border point – a point is within the ε radius of a core point BUT has less than the minimum number of other points (minPts) within its own ε radius
Noise point – a point that is neither a core point or a border point.
DBSCAN discovers clusters as dense areas in space, surrounded by sparser areas. Points in the sparse areas are usually considered noise (needs there to be drop-offs in density to detect cluster borders).
Using Scikit-Learn, I trained a model to cluster the points. Converting to radians seemed to be a simpler choice as I was getting incorrect clustering when I converted the lat/long to cartesian coordinates. However, I seemed to get decent accuracy when working with radians so I stuck with it.

More on queries can be found (here.)[https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL]


#### Further Reading
[Overpy, a Python Wrapper for the Overpass API](https://python-overpy.readthedocs.io/en/latest/introduction.html)

[Haversine Distance](https://community.esri.com/groups/coordinate-reference-systems/blog/2017/10/05/haversine-formula#targetText=For%20example%2C%20haversine(%CE%B8,longitude%20of%20the%20two%20points.)

Another potential approach is highlighted (here)[https://gis.stackexchange.com/questions/11567/spatial-clustering-with-postgis] and (here.)[https://gis.stackexchange.com/questions/270269/using-st-clusterdbscan-on-results-of-st-clusterkmeans-for-nested-clustering-with]