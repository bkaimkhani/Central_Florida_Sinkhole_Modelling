# Central Florida Sinkhole Susceptibility Mapping

Machine learning pipeline for predicting sinkhole susceptibility across six Central Florida counties. Seven classifiers are trained and evaluated using 13 hydrogeological and topographic conditioning factors. Best model: **Random Forest** with AUC-ROC 0.891 and accuracy 80.56%.

---

## Repository Structure

```
Central_Florida_Sinkhole_Modelling/
│
├── Sinkhole_Susceptibility_ML.ipynb   # Full ML pipeline notebook
├── Sinkholes_data.csv                 # Labeled dataset (5,759 samples)
│
└── SIR_Positive/                      # Shapefiles — FGS confirmed sinkhole locations
    └── *.shp, *.dbf, *.shx, ...
```

The shapefile folder contains ArcGIS-compatible vector layers for the positive sample locations used in model training.

---

## Dataset

**File:** `Sinkholes_data.csv`  
**Samples:** 5,759 (2,900 positive, 2,859 negative)  
**Class balance:** 50.4% / 49.6%

| Column | Description |
|---|---|
| `Point_ID` | Unique sample identifier |
| `Label` | 1 = sinkhole (positive), 0 = stable ground (negative) |
| `Annual_Precipitation` | Mean annual precipitation (mm) |
| `Distance_to_Nearest_Karst_Feature` | Euclidean distance to nearest karst feature (m) |
| `Distance_to_Nearest_Water_body` | Euclidean distance to nearest water body (m) |
| `Elevation_(m)` | Ground surface elevation (m) |
| `Hydrualic_Head_Difference` | Difference in hydraulic head between aquifer units |
| `IAS_Thickness` | Intermediate Aquifer System thickness (m) |
| `LULC` | Land Use and Land Cover class code |
| `Overburden_Thickness` | Thickness of unconsolidated material above limestone (m) |
| `SAS_Thickness` | Surficial Aquifer System thickness (m) |
| `Shear_Waves_Velocities` | Shear wave velocity (m/s) |
| `Slope` | Surface slope (degrees) |
| `Surface_Geology` | Surface geology class code |
| `TPI` | Topographic Position Index |

Positive samples are sourced from the Florida Geological Survey (FGS) Subsidence Incident Report database. Negative samples are generated using a spatially controlled pseudo-absence protocol with a 500 m exclusion buffer and 5,000 m outer boundary to prevent label noise and covariate shift.

---

## Models Evaluated

| Model | Accuracy | AUC-ROC |
|---|---|---|
| Random Forest | 80.56% | 0.891 |
| Extra Trees | 79.34% | 0.888 |
| Gradient Boosting | 80.03% | 0.884 |
| Multilayer Perceptron | 79.08% | 0.868 |
| Support Vector Machine | 78.47% | 0.865 |
| AdaBoost | 75.26% | 0.834 |
| Logistic Regression | 69.53% | 0.752 |

---

## Requirements

```
scikit-learn
pandas
numpy
matplotlib
seaborn
```

Install with:

```bash
pip install scikit-learn pandas numpy matplotlib seaborn
```

---

## Usage

Open `Sinkhole_Susceptibility_ML.ipynb` in Jupyter and run all cells. The notebook loads `Sinkholes_data.csv` from the same directory by default.

---

## License

This repository is shared for academic purposes. Data sourced from the Florida Geological Survey (FGS), United States Geological Survey (USGS), Southwest Florida Water Management District (SWFWMD), NOAA PRISM Climate Group, and Florida Natural Areas Inventory (FNAI).
