# Assignment 1 — Geospatial Data and Route Search

Part II (coding exercises) of ISE 571 Assignment 1.

**Notebook:** [`geospatial_routing.ipynb`](geospatial_routing.ipynb) · [open in Colab](https://colab.research.google.com/github/besology512/ISE571-Heuristic-Search-Methods/blob/main/assignment1/geospatial_routing.ipynb)

## Contents

1. **Dataset.** 2,495 points of interest in 134 districts of the Dammam metropolitan area (Dammam, Khobar, Dhahran), from OpenStreetMap, grouped into nine service categories. The two routing end points are geocoded with Nominatim.
2. **Visualisation.** Choropleth, non-contiguous cartogram, bubble map, hexagonal binning, kernel-density heat map and DBSCAN / marker-cluster maps, each followed by its observations.
3. **Points of interest.** KFUPM and the Mall of Dhahran.
4. **Routing.** BFS, DFS, Dijkstra, A\*, hill climbing and simulated annealing, all implemented from scratch on the OSM drivable network (2,749 nodes), compared by route length and run time, plus a robustness check on 30 random trips.

## Main result (KFUPM → Mall of Dhahran)

| Algorithm | Route length | Gap | Time | Nodes expanded / evaluations |
|---|---:|---:|---:|---:|
| BFS | 3,006 m | 0.0 % | 0.09 ms | 245 |
| DFS | 52,934 m | 1,661 % | 0.8 ms | 1,299 |
| Dijkstra | 3,006 m | 0.0 % | 0.3 ms | 259 |
| A\* | 3,006 m | 0.0 % | 0.1 ms | 51 |
| Hill climbing (10 seeds) | 3,006 m | 0.0 % | ≈ 0.6 s | 461 |
| Simulated annealing (10 seeds) | 3,006 m | 0.0 % | ≈ 2.1 s | 1,721 |

On 30 random trips, Dijkstra and A\* were always optimal. SA was optimal on 14 trips (median gap 0.04 %), HC on 9 (median gap 1.9 %), BFS on 6 and DFS on none. Timings come from one laptop run and will vary from machine to machine.

## Interactive maps

The Folium maps are in [`maps/`](maps) and can be viewed in the browser:

* [Routes of all six algorithms](https://raw.githack.com/besology512/ISE571-Heuristic-Search-Methods/main/assignment1/maps/routes.html)
* [Points of interest](https://raw.githack.com/besology512/ISE571-Heuristic-Search-Methods/main/assignment1/maps/points_of_interest.html)
* [Choropleth](https://raw.githack.com/besology512/ISE571-Heuristic-Search-Methods/main/assignment1/maps/choropleth.html) · [Heat map by category](https://raw.githack.com/besology512/ISE571-Heuristic-Search-Methods/main/assignment1/maps/heatmap.html) · [Marker clusters](https://raw.githack.com/besology512/ISE571-Heuristic-Search-Methods/main/assignment1/maps/cluster_map.html)

## Layout

```
assignment1/
├── geospatial_routing.ipynb   notebook (committed with outputs)
├── data/                      cached OSM districts, POIs, road graph, geocodes, result tables
├── figures/                   static figures exported by the notebook
└── maps/                      interactive Folium maps (HTML)
```

## Reproducing

```bash
pip install -r ../requirements.txt
jupyter nbconvert --to notebook --execute --inplace geospatial_routing.ipynb
```

When `data/` is present, the notebook runs fully offline except for basemap tiles. If you delete it, the notebook downloads fresh OSM data, and the counts may differ slightly because OpenStreetMap is continuously edited.

Data © OpenStreetMap contributors (ODbL). Basemap tiles © Esri.
