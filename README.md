# Urban Food Hotspots Analysis (Zomato Bangalore)

**Author:** Ashwini Ranganath
**Programme:** MSc Data Science, University of East London (UEL)

## About this project

This project looks at where restaurants tend to cluster across Bangalore, using data from Zomato. The idea was to move beyond just listing where restaurants are and actually test whether there are statistically meaningful "hotspots" — areas where restaurant ratings are consistently higher (or lower) than you'd expect by chance.

The analysis follows the CRISP-DM framework and uses restaurant coordinates and ratings as the main inputs.

## Hotspot maps

All maps below are interactive — open the `.html` files to zoom, pan, and click on clusters for details.

- [Restaurant density heatmap](outputs/heatmap.html)
- [DBSCAN clusters](outputs/dbscan_hotspot_map.html)
- [HDBSCAN clusters](outputs/hdbscan_hotspot_map.html)
- [K-Means clusters](outputs/kmeans_hotspot_map.html)
- [LISA hotspot map (final result)](outputs/lisa_hotspot_map.html)

## Choosing a clustering method

I tested a few different clustering approaches before settling on one:

- **K-Means** struggled here because it assumes clusters are roughly spherical and similar in size, which doesn't really match how restaurants are distributed across a real city.
- **DBSCAN** was better, but it relies on a single density threshold applied everywhere, and restaurant density varies a lot between areas like Koramangala and quieter parts of the city.
- **HDBSCAN** ended up working best, since it can adapt to varying densities and handle noise more gracefully than the other two.

## Spatial autocorrelation

To check whether ratings are spatially patterned rather than random, I ran a Global Moran's I test:

- I = 0.1837, p = 0.011

This came back statistically significant, meaning restaurants with similar ratings do tend to sit near each other rather than being scattered randomly across the city.

## Where the hotspots are

Using LISA (Local Indicators of Spatial Association), three areas came out as significant High-High clusters — meaning they're highly rated and surrounded by other highly rated restaurants:

- Indiranagar
- Koramangala
- BTM Layout

## Why this matters

A few practical uses for this kind of analysis:

- **Business** – helps identify where competition is already dense, and where there might be room to expand.
- **Logistics** – useful for planning delivery zones and deciding where to place driver or delivery hubs.
- **Recommendations** – spatial patterns like this can feed into location-aware restaurant recommendation systems.

## Dataset

- Source: [Zomato Bangalore Restaurants](https://www.kaggle.com/datasets/himanshupoddar/zomato-bangalore-restaurants) dataset on Kaggle (not included in this repo due to file size — download it from the link above)
- Size: 56,201 rows × 17 columns
- Fields used: restaurant name, latitude, longitude, rating

## Repo structure

```
├── notebooks/     analysis notebooks
├── outputs/       maps, plots, exported results
├── requirements.txt
└── README.md
```

> Note: the raw dataset isn't included in this repo due to its size (~770MB). See the Dataset section above for the download link.

## Running this locally

```bash
git clone https://github.com/Ashwini2591/urban-food-hotspot-clustering.git
cd urban-food-hotspot-clustering
pip install -r requirements.txt
jupyter notebook notebooks/analysis.ipynb
```

## License

MIT License — see the LICENSE file for details.
