# Setup

The code is composed as an R Markdown document `nitrogen_wheat.Rmd`. This has been written and tested with the following system and software versions:

```         
MacBook Air M1, 2020 running macOS Ventura 13.2.1
RStudio Version 2023.09.0+463
R 4.2.1
```

After installing R (and RStudio), to ensure that the code can be executed, the following packages should be installed (the versions specified are those that were used to compose the code):

```         
terra=1.7.55
sf=1.0.14
sp=2.1.0
ggplot2=3.4.4
dplyr=1.1.3
tidyr=1.3.0
rasterVis=0.51.5
knitr=1.44
rmarkdown=2.25
```

These packages can be installed using such commands:

```         
install.packages("terra", version="1.7.55")
install.packages("sf", version="1.0.14")
```

If you don't want to specify the version, you can just use `install.packages("terra")` and so on.

The input data is in the folder `data,` which isn't included as a part of this repository, can be accessed from [here](https://www.dropbox.com/sh/uv3qzqvs45j7gup/AAAfkMPVTOQnaP4JXOKuaA7Xa?%20dl=0). Download this and put the three folders into a single folder called `data`.

The outputs (raster files and plots) are stored in a folder called `outputs`. This is already present in the repository and also contains, in addition, three PNG files of the plots for easier display.

# How to run

The R Markdown file `nitrogen_wheat.Rmd` can be run in RStudio (or another IDE like Visual Studio Code) either chunk by chunk, or can be run altogether using `knitr` into an output HTML (`nitrogen_wheat.html`) or PDF file. Running the code chunk by chunk will load all the variables and packages into R's active memory, while using `knitr` will directly generate an output HTML or PDF file without giving you access to the variables. Which chunks to run, and what to write to the output HTML or PDF file can be controlled using various options along with individual chunks. On the other hand, running the code chunk by chunk gives you greater access to what to run and see how the code works in a more modular fashion. However, both ways of running the code would generate all the output files and plots written as part of the code - raster files and plots of wheat production, nitrogen output in wheat, nitrogen losses and outputs for the top 10 countries, etc.

When using `knitr`, ensure that the first code chunk `setup` has the option `eval=TRUE` so that all further code chunks (unless they individually have `eval=FALSE` will be run when run using `knitr`. By default, `eval=FALSE` in the code chunk called `setup`. Only the code chunks which load the libraries, read in the data and display tables are set to be evaluated with `eval=TRUE`. Of course, you can change any of these as per your requirements.

# Answers to questions

## Question 1

1. Global map of wheat production volume in million tons (Mt) - `outputs/Wheat_produced.pdf` and `outputs/Wheat_produced.png`
2. Raster file (GeoTIFF) of wheat production volume - `outputs/wheat_production_Mt.tif`

## Question 2

1. Wheat production at country level - `outputs/wheat_production_Mt_by_country.csv`

## Question 3

1. Raster file (GeoTIFF) of nitrogen output as 2% of harvested wheat - `outputs/nitrogen_output_Mt.tif`
2. Global map of nitrogen output as 2% of harvested wheat - `outputs/Nitrogen_output.pdf` and `outputs/Nitrogen_output.png`

## Question 4 - Main patterns of nitrogen losses across countries

a. Nitrogen inputs, outputs and losses of top 10 wheat producing countries - `outputs/top10_countries_nitrogen.csv`
b. Summary figure for nitrogen outputs and losses of top 10 countries - `outputs/Nitrogen_output_loss.pdf` and `outputs/Nitrogen_output_loss.png`
c. China and India, the top two countries with the highest wheat production volumes, are also the countries with the largest nitrogen losses, suggesting that higher production can lead to more significant nitrogen losses. However, for the third largest producer of wheat, the USA, nitrogen loss is comparatively lower, suggesting better nitrogen management and/or efficient utilization. France, ranked 5, has the least relative losses, indicating excellent nitrogen management. On the other, Pakistan, ranked 8, experiences the greatest relative losses, indicating potential inefficiencies in nitrogen utilization. Interestingly, the USA and Pakistan have very similar nitrogen inputs but the USA, with better nitrogen management, has significantly larger nitrogen in its harvested wheat compared to Pakistan.

## Question 5

Incorporating such analysis of nitrogen utilization via wheat production into BNR's modeling suite GLOBIOM could provide a more nuanced understanding of nitrogen dynamics at the country level, helping policymakers target interventions for sustainable agricultural practices. By analyzing nitrogen losses in relation to production volume and NUE, GLOBIOM can refine its predictions on land-use change, agricultural trade, and emissions in response to potential policy measures. However, potential limitations include the accuracy and granularity of input data, and the ability of the model, especially in the context of the assumption-based calculations (e.g., a fixed percentage of nitrogen content in harvested yield) to capture all real-world complexities and interactions between nitrogen dynamics and other environmental and socio-economic factors.

## Question 6

One issue was the mismatch in country names between the GAUL dataset and the NUE dataset. While the GAUL dataset has 273 countries, the NUE dataset has only 113 countries, and out of these 113, only 90 countries have names that exactly match country names in the GAUL dataset. The USA and Russia, two countries among the top 10 wheat producing countries, are among the 23 that don't match in country names. While I manually changed the names of these two countries to ensure compatibility, a similar work on the whole dataset might require either more manual work, or the use of fuzzy string matching methods.
