# Origin and Distribution of the Intraplate Magmatism of South America

**Authors:** Bruna Chagas de Melo, Sergei Lebedev, Sally Gibson, Joost de Laat, Nicola Celli, Marcelo Assumpção

**Journal:** [placeholder]

**DOI:** [placeholder]

## Abstract

The South American platform experienced significant Mesozoic and Cenozoic intraplate volcanism. Using the new high-resolution S-wave velocity tomographic model SACI-24 and an extensive magmatism dataset, we show that intraplate magmatism across South America derives from a single deep mantle plume beneath the continent. Its distribution is controlled by plume-lithosphere interaction and lateral transport along gradients in lithospheric thickness.

## Repository Structure

```
publication/
  data/
    magmatism/           Igneous rock locations and compiled dataset
    hotspots/            Hotspot catalogues and labels
    motion_paths/        Reconstructed hotspot tracks
    flood_basalts/       CAMP and Parana thickness contours
    contours/            LIP outlines, cratons, oceanic features
    dikes/               Mafic dike swarms
    plate_boundaries/    Plate boundary models
    ridges/              Mid-ocean ridge segments
    kimberlites/         Kimberlite and carbonatite data
    seismic_model/       SACI-24 tomographic model (NetCDF)
  code/
    gmt/                 GMT 6 scripts for Figures 1, 3, 5, 7
    python/              Jupyter notebooks for Figures 6 and Supp. Fig. 1
  figures/               Output directory (not tracked)
```

## Dataset Provenance

### Compiled Magmatism Dataset

`data/magmatism/SA_intraplate_magmatism.csv` is the main compiled dataset (429 entries) with columns: `longitude, latitude, age_ma, age_error_ma, rock_type, dating_method, reference`. It merges data from three sources listed below.

### Source Datasets (Table 1 of manuscript)

| File | Data type | Reference |
|------|-----------|-----------|
| `data/magmatism/SA_intraplate_magmatism.csv` | Compiled igneous rock locations | This study |
| `data/magmatism/igneous_rocks_all.txt` | Merged locations (lon, lat, age, ref) | Mizusaki et al. (2002), Ribeiro et al. (2018), Tassinari (1996) |
| `data/hotspots/hotspots_whittaker2015.xy` | Present-day hotspot catalogue | Whittaker et al. (2015) |
| `data/motion_paths/motion_path_*_Muller2016_*.xy` | Reconstructed hotspot tracks | Muller et al. (2016) |
| `data/motion_paths/motion_path_*_Matthews2016_*.xy` | Reconstructed hotspot tracks | Matthews et al. (2016) |
| `data/motion_paths/motion_path_*_Seton2012_*.xy` | Reconstructed hotspot tracks | Seton et al. (2012) |
| `data/flood_basalts/camp_demin_*.txt` | CAMP sill thickness contours | de Min et al. (2003) |
| `data/flood_basalts/parana_peate_*.txt` | Parana basalt thickness contours | Peate et al. (1992) |
| `data/contours/camp_outline.txt` | CAMP province contour | Heimdal et al. (2018); de Min et al. (2003) |
| `data/contours/serra_geral_outline.txt` | Serra Geral province contour | Zalan (1987) |
| `data/contours/*_kay2007.txt` | Patagonian igneous province contours | Kay et al. (2007) |
| `data/dikes/dikes_*_pessano2021.txt` | Mafic dike swarms | Pessano et al. (2021) |
| `data/plate_boundaries/bird2003.txt` | Digital plate boundary model | Bird (2003) |
| `data/kimberlites/kimberlites_tappe2018.csv` | Kimberlite compilation | Tappe et al. (2018) |
| `data/kimberlites/carbonatites_woolley2008.csv` | Carbonatite occurrences | Woolley & Kjarsgaard (2008) |
| `data/seismic_model/SACI-24.nc` | S-wave velocity tomography | Chagas de Melo et al. (2025) |

## SACI-24 Tomographic Model

The SACI-24 model (`data/seismic_model/SACI-24.nc`) is a global S-wave velocity model parameterized on a triangular grid (~120 km lateral knot spacing) with depth nodes at 7, 20, 36, 56, 80, 110, 150, 200, 260, 330, 410, 485, 585, 660, 809, and 1007 km. Velocity perturbations are in percent relative to a 1D reference model. The model is also available from the IRIS Earth Model Collaboration (EMC).

## Software Requirements

### GMT figures (Figures 1, 3, 5, 7)
- [GMT 6.x](https://www.generic-mapping-tools.org/) (modern mode)
- Bash or Zsh shell

### Python figures (Figure 6, Supplementary Figure 1)
- Python 3.9+
- Install dependencies: `pip install -r code/python/requirements.txt`
- Required packages: pygmt, gplately, xarray, numpy, matplotlib, plate-model-manager

## Reproducing Figures

All GMT scripts auto-detect the repository root via `REPO_ROOT` and use relative paths. Run from the `code/gmt/` directory:

```bash
cd code/gmt/

# Figure 1: Main magmatic provinces map
./fig1_magmatic_provinces.gmt -l fill -m 200 -t 200

# Figure 3: S-wave velocity anomaly maps
./fig3_velocity_maps.gmt

# Figure 5: Hotspot tracks on lithosphere
./fig5_hotspot_tracks.gmt

# Figure 7: Cross-section model comparison
# NOTE: Requires external model data from SubMachine (see below)
./fig7_model_comparison.gmt
```

For Python notebooks, run from `code/python/`:
```bash
cd code/python/
jupyter notebook fig6_delamination.ipynb
jupyter notebook supp_tristan_tracks.ipynb
```

### External Model Data for Figure 7

Figure 7 compares SACI-24 with whole-mantle models SPiRaL (Simmons et al., 2021), UU-P07 (Amaru, 2007), and SEMum2 (French & Romanowicz, 2015). Cross-section data for these models can be extracted from [SubMachine](https://www.earth.ox.ac.uk/~smachine/cgi/index.php) and placed in `data/external_models/`.

## Data Availability Statement

The seismic tomography model SACI-24 is available from the IRIS Earth Model Collaboration (EMC) and is included in this repository. Igneous rock occurrence data were compiled from Mizusaki et al. (2002), Ribeiro et al. (2018), and Tassinari (1996). Hotspot locations follow the compilation of Whittaker et al. (2015). Plate boundaries are from Bird (2003). Mafic dike swarm data are from Pessano et al. (2021). Continental flood basalt thickness data for the Parana province are from Peate et al. (1992) and for CAMP sills from de Min et al. (2003). Plate reconstructions use the models of Muller et al. (2016), Matthews et al. (2016), and Seton et al. (2012), accessed through GPlately. Patagonian igneous province contours are from Kay et al. (2007). Kimberlite data are from Tappe et al. (2018). Carbonatite data are from Woolley & Kjarsgaard (2008). All datasets and figure-generating scripts are archived at [Zenodo DOI] and available at [GitHub URL].

## License

- Data: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)
- Code: [MIT License](LICENSE)
