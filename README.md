# Global Continental Residual Topography

This repository contains estimates of global residual topography after correcting elevation for
crustal thickness and density variations.  It constitutes the results of Stephenson _et al._ (2024).
A full methodological description can be found in that paper.  '_Residual topography_' is topography supported by mantle buoyancy structure after having crustal isostatic topography removed.  The crustal thickness database used to calculate these reisudal topographic estimates is [`SeisCruST`](https://github.com/sstephenson2/SeisCRUST), a global seismic crustal thickness and structure database.  Crustal density calculations are carried out using [`SMV2rho`](https://github.com/sstephenson2/SMV2rho), a package designed to estimate cotinental crustal density from seismic velocity profiles.

## NOTE

Crustal thickness estimates are taken from a large database of estimates of crustal thickness and velocity determined by a variety of seismic experiments.  If using the crustal thickness, velocity or density information provided here, it is imperative that the user refer to the documentation in [`SeisCruST`](https://github.com/sstephenson2/SeisCRUST) and properly reference both that package and the individual authors whose work is included in the compilation.


## Binned residual topographic estimates

The `BINNED_RESIDUAL_ELEVATION/` directory contains data where the residual topography has been averaged into bins of 1, 2, 3, and 4 degrees. 

The data is organized into the following columns:

| Column Name | Description |
| --- | --- |
| `lon` | Longitude |
| `lat` | Latitude |
| `t_c` | Depth of the Mohorovičić discontinuity (the boundary between the Earth's crust and mantle) |
| `residual_elevation` | Residual elevation |
| `residual_elevation_error` | Error in the residual elevation |

## Pointwise residual topographic estimates

The `POINTWISE_RESIDUAL_ELEVATION/` directory contains station-by-station residual topgoraphic estimates with uncertainties.  IIt also contains geophysical parameters exracted locally to the station from global grids.  The structure is as follows:

| Column Name | Description |
| --- | --- |
| `station` | The identifier for the station where the data was collected (NaN if no velocity profile present). |
| `lon` | Longitude of the station. |
| `lat` | Latitude of the station. |
| `t_c` | Depth to Moho. |
| `vp` | Bulk P-wave velocity. |
| `vs` | Bulk S-wave velocity. |
| `rho_c` | Density of the crust calculated using temperature dependent version of `SMV2rho`. |
| `ETOPO` | Topographic elevation. |
| `ETOPO_filt_30km` | Topographic elevation filtered for wavelengths > 30 km. |
| `tl` | Lithospheric thickness taken from Hoggard _et al._ (2021) at the station. |
| `long_lam_grav` | Long-wavelength free air gravity anomaly at the station. |
| `thickness_correction` | Crustal thickness correction |
| `density_correction` | Crustal density correction |
| `residual_topography` | Residual topographic estimate |
| `dens_err_all` | Crustal density error |
| `res_topo_err` | Residual topography error |
| `dens_corr_err` | Crustal density correction error |
| `thickness_corr_err` | Crustal thickness correction error |

## Input crustal files

Located in `INPUT_CRUST_FILES/`.  Here the input crustal thickness and density data can be found, as well as several other geophysical parameters extracted locally from various grids at the site of each data point.

#### Crustal database

This data file `station_lon_lat_vp_vs_rho_topo_filt_lith_grav_all_onshore.dat` contains pointwise crustal thickness, velocity and density estimates as well as geophysical parameters extracted locally from various grids at each data point.  Velocity and density is taken from [`SeisCruST`](https://github.com/sstephenson2/SeisCRUST) and [`SMV2rho`](https://github.com/sstephenson2/SMV2rho).  Please refer to documentation for these packages for more information. The columns in the file are described as follows:

| Column Name | Description |
| --- | --- |
| `station` | The identifier for the station where the data was collected (NaN if no velocity profile present). |
| `lon` | Longitude of the station. |
| `lat` | Latitude of the station. |
| `t_c` | Depth to Moho. |
| `vp` | Bulk P-wave velocity. |
| `vs` | Bulk S-wave velocity. |
| `rho_c` | Density of the crust calculated using temperature dependent version of `SMV2rho`. |
| `ETOPO` | Topographic elevation. |
| `ETOPO_filt_30km` | Topographic elevation filtered for wavelengths > 30 km. |
| `tl` | Lithospheric thickness taken from Hoggard _et al._ (2021) at the station. |
| `long_lam_grav` | Long-wavelength free air gravity anomaly at the station. |

#### Sea level reference model

`sea_level_points.dat` contains the subset of points within 25 m of sea level.

## Scripts

The `SCRIPTS/` directory contains useful processing and plotting routines.

#### Residual topography calculation notebook

`calc_residual_topography_crust_only.ipynb` contains a notebook to calculate continental residual topography.  It also contains some useful plots and processing to remove outliers that are fully described in Stephenson _et al._ (2024).

#### Residual topography binning

`bin_residual_topography.gmt` contains a shell or `gmt` script to average residual topography into $1\times1$ degree bins and then calculate some useful statistics on the binned results.

#### Excision polygons

`excision_polys_combined.ll` contains polygons to mask out parts of the world where flexure or orogenesis may be a significant control on topography.

## License

The package is distributed under an MIT license.