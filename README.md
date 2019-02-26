# Intro

 This is a minimal example of a book based on R Markdown and [bookdown](https://github.com/rstudio/bookdown). Please see the page "Get Started" at [https://bookdown.org/](https://bookdown.org/) for how to compile this example.
 
[Course Webiste](https://broadinstitute.github.io/2019_scWorkshop/)


## Docker Usage

There is a docker image that goes along with this course.  The following explains how to use the docker image and what software it contains.  

### Installing Docker

Make sure to have docker installed on your computer. Go to the docker getting started [website](https://www.docker.com/get-started) and select the download for your operating system.  


### Software Included

All additional software is included in the /usr/local/src directory inside the docker container.  

  - [STAR](https://github.com/alexdobin/STAR)
  - [Cellranger](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/installation)
  - [FASTQC](https://www.bioinformatics.babraham.ac.uk/projects/download.html)
  - [Samtools](https://github.com/samtools/samtools)
  - [IGV](http://software.broadinstitute.org/software/igv/)
  - [CITE-seq Count](https://github.com/Hoohm/CITE-seq-Count)
  - [R/Rstudio](https://www.rstudio.com/)
  
  
### Pull Image

The first thing you will need to do is pull the docker image to your computer.  You do this by running the command:

```{bash}
docker pull kdgosik/scellbern2019:latest
```

### Running Rstudio in Docker

```{bash}
sudo docker run --rm -it -e PASSWORD=train \
-v $PWD/Share:/Share \
-v $PWD:/mydir \
-p 9000:8787 kdgosik/scellbern2019 bash
```
ec2-<AWS PUBLIC IP ADDRESS>.us-west-2.compute.amazonaws.com:<PORT NUMBER>
ec2-54-202-32-102.us-west-2.compute.amazonaws.com:9000


**Explaination of commands**
  - docker: command to run docker
  - run: asking docker to run a container
  - --rm: flag to remove the container when you exit from it
      - nothing will be saved from your session to access again later
      - this flag can be removed to keep container
  - -it: flag to run the container interactively
    - this will keep all session output displaying on the terminal
    - to stop container go to terminal and press Crtl+c
  - -e PASSWORD=train: password assignment you will need to access rstudio when you login
  - -p 9000:8787: flag to assign port mapping.
    - rstudio runs on port 8787 inside the container
    - you will access rstudio by going to port 9000 on your computer (localhost:9000 in your browser)
    - 9000 can be any port you would like.  We will change this up for each student in the class
  - kdgosik/scellbern2019: the image to run.  It will be the image into a container if not already built on your computer
    - [image link](https://hub.docker.com/r/kdgosik/scellbern2019)


#### Accessing Rstudio
Once you run the docker run command above, you can go to your browser at localhost:9000.  This will bring you to a log-in screen for rstudio.  Enter the username: rstudio and password: train.  This will log you into Rstudio where you can do your analysis.  After this you can install whichever R packages you would like.  


**examples**
```{R}
## CRAN Packages
install.packages("ggplot2")
install.packages("gam")
install.packages("ggbeeswarm")
install.packages("ggthemes")
install.packages("dplyr")
install.packages("plyr")
install.packages("Matrix")
install.packages("fossil")
install.packages("Seurat")
install.packages("BiocManager")
install.packages("devtools")
install.packages('umap')
install.packages('rmarkdown')

## Bioconductor Packages
BiocManager::install("SingleCellExperiment", version = "3.8", update = FALSE)
BiocManager::install("destiny", version = "3.8", update = FALSE)
BiocManager::install("slingshot", version = "3.8", update = FALSE)
BiocManager::install("splatter", version = "3.8", update = FALSE)
BiocManager::install("scater", version = "3.8", update = FALSE)
BiocManager::install("DropletUtils", version = "3.8", update = FALSE)
BiocManager::install("pcaMethods", version = "3.8", update = FALSE)

## Github Packages
devtools::install_github("broadinstitute/inferCNV")
devtools::install_github("velocyto-team/velocyto.R")
devtools::install_github('MacoskoLab/liger')
```

### Docker Terminal

Same command as above but add the option bash at the end to access the ternimal in the docker container.

```{bash}
docker run --rm -it -v $PWD/Share:/Share -v $PWD:/mydir kdgosik/scellbern2019 bash
```
