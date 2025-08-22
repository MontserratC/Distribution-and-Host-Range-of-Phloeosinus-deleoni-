# Repository Description

This repository accompanies a manuscript currently under review, in which the methodology of ecological niche modeling with Maxent was applied using the kuenm package in R (Cobos et al., 2019).
The main objective of the study was to calibrate, evaluate, and select ecological niche models for a species of interest, integrating occurrence data, environmental variables, and statistical performance criteria to obtain robust predictions of its potential distribution.

The repository includes:
Occurrence datasets: training, testing, and full dataset.
Environmental variables in raster format.
R scripts that allow full reproduction of the workflow transparently:
Calibration of candidate models (kuenm_cal)
Model evaluation and selection (kuenm_ceval)
Calibration and evaluation results, ready for further analysis or visualization.
The implemented methodology strictly follows the guidelines of Cobos et al. (2019), including:
Generation of multiple candidate models with different regularization multipliers and combinations of feature classes.
Model evaluation based on criteria such as AICc and prediction thresholds.
Selection of the most robust models according to statistical performance and generalization.

# Uso de kuenm

Este repositorio contiene un script en **R** que implementa la metodología de **Cobos et al. (2019)** usando el paquete [kuenm](https://github.com/marlonecobos/kuenm).  
El flujo de trabajo sigue los pasos para calibrar, evaluar y seleccionar modelos de nicho ecológico en **Maxent**.
Para seguir el tutorial completo entre al link anterior

> **Referencia principal**:  
> Cobos, M. E., Peterson, A. T., Barve, N., & Osorio-Olvera, L. (2019). kuenm: an R package for detailed development of ecological niche models using Maxent. *PeerJ*, 7, e6281. https://doi.org/10.7717/peerj.6281  

---
## 🛠 Prerequisites
## 🛠 Requisitos previos
To run this analysis, you will need:

R (version 4.0 or higher recommended)

RStudio (optional, but recommended for convenience)

R packages: kuenm, raster, purrr

Para ejecutar este análisis necesitas:

- **R** (versión 4.0 o superior recomendada)  
- **RStudio** (opcional, pero recomendado para mayor comodidad)  
- Paquetes de R: `kuenm`, `raster`, `purrr`  

---
## 💾 Package Installation
## 💾 Instalación de paquetes

```r
# Instalar paquetes desde CRAN
install.packages(c("raster", "purrr"))

# Instalar kuenm desde CRAN
install.packages("kuenm")
library(kuenm)
library(raster)
library(purrr)

```

## Setting the Working Directory

Make sure to place your occurrence files and environmental variables in a specific folder, then set that directory in R:
##Configuración del directorio de trabajo

Asegúrate de colocar tus archivos de ocurrencias y variables ambientales en un directorio específico, y luego define ese directorio en R:
```r
setwd("TU/DIRECTORIO/DE/TRABAJO")
-setwd("YOUR/WORKING/DIRECTORY")
```
## 📂 File Structure

The script uses three occurrence datasets and a set of environmental variables:

- `deleoni_joint.csv` → all occurrences
- `deleoni_train.csv` → training data 
- `deleoni_test.csv` → test data 
- `M_variables/` → folder containing environmental variables (raster)

The output folders are generated automatically:
- `Candidate_Models/`→ calibrated models 
- `Calibration_results/`  → model evaluations

## 📂 Estructura de archivos

El script utiliza tres conjuntos de datos de ocurrencia y un conjunto de variables ambientales:

- `deleoni_joint.csv` → todas las ocurrencias  
- `deleoni_train.csv` → datos de entrenamiento  
- `deleoni_test.csv` → datos de prueba  
- `M_variables/` → carpeta con las variables ambientales (raster)  

Las carpetas de salida se generan automáticamente:

- `Candidate_Models/` → modelos calibrados  
- `Calibration_results/` → evaluaciones de modelos  

---

## 🚀 Usage Instructions- Instrucciones de uso

1. ##Code Workflow-Flujo del código
1. Model Calibration - Calibración de modelos

```r
kuenm_cal(
  occ.joint = "deleoni_joint.csv",
  occ.tra = "deleoni_train.csv",
  M.var.dir = "M_variables",
  batch = "Candidate_models",
  out.dir = "Candidate_Models",
  reg.mult = c(0.5, 1, 2),
  f.clas = c("l", "lq", "lqp"),
  args = NULL,
  maxent.path = ".",
  wait = FALSE,
  run = TRUE
)
```

2. Model Evaluation and Selection- Evaluación y selección de modelos
```r
kuenm_cal(occ.joint = occ_joint, occ.tra = occ_tra, M.var.dir = M_var_dir, batch = batch_cal,
out.dir = out_dir, reg.mult = reg_mult, f.clas = f_clas, args = args,
maxent.path = maxent_path, wait = wait, run = run)
M_var_dir <- "M_variables"
batch_cal <- "Candidate_models"
out_dir <- "Candidate_Models"
reg_mult <- c(0.5,1,2)
f_clas <- c("l", "lq","lqp") # alternativamente "all"
args <- NULL # e.g., "maximumbackground=20000" for increasing the number of pixels in the background or
# note that some arguments are fixed in the function and should not be changed
maxent_path <- "." # path de maxent
wait <- FALSE
run <- TRUE
## ----eval=FALSE----------------------------------------------------------------------------------------
kuenm_cal(occ.joint = occ_joint, occ.tra = occ_tra, M.var.dir = M_var_dir, batch = batch_cal,
out.dir = out_dir, reg.mult = reg_mult, f.clas = f_clas, args = args,
maxent.path = maxent_path, wait = wait, run = run)
occ_test <- "deleoni_test.csv"
out_eval <- "Calibration_results"
threshold <- 5
rand_percent <- 50
iterations <- 100
kept <- TRUE
selection <- "OR_AICc"
paral_proc <- TRUE
cal_eval <- kuenm_ceval(path = out_dir, occ.joint = occ_joint, occ.tra = occ_tra,
occ.test = occ_test, batch = batch_cal,
out.eval = out_eval, threshold = threshold,
rand.percent = rand_percent, iterations = iterations,
kept = kept, selection = selection,
parallel.proc = paral_proc)
```


Bibliography

Cobos, M. E., Peterson, A. T., Barve, N., & Osorio-Olvera, L. (2019). kuenm: an R package for detailed development of ecological niche models using Maxent. PeerJ, 7, e6281.
