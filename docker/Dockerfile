# Docker base image
FROM rocker/tidyverse:4.1.1
# FROM bioconductor/bioconductor_docker:RELEASE_3_13

# information
LABEL version="yyyymmdd.vv"
LABEL description="Docker RStudio"
LABEL maintainer="xxxxxxxx@xxxxx.xxx"

# update/install apt package and Japanese font (IPAex)
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ssh \
    libxt-dev \
    libxml2-dev \
    libgit2-dev \
    fonts-ipaexfont \
  && apt-get clean

# OS env JP locale (Character, DateTime)
ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
RUN sed -i '$d' /etc/locale.gen \
  && echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen ja_JP.UTF-8 \
    && /usr/sbin/update-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
RUN /bin/bash -c "source /etc/default/locale"
RUN ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# install Japanese font
RUN apt-get update && apt-get install -y \
  fonts-ipaexfont \
  fonts-noto-cjk

ENV R_REMOTES_NO_ERRORS_FROM_WARNINGS=true

# change directory
WORKDIR /home/rstudio/rproject

# Install R packages
# RUN install2.r pkgname1 pkgname2
# RUN Rscript -e "install.packages('vector_of_package_names')"
# RUN Rscript -e 'BiocManager::install("vector_of_package_names")'
# example code (below):
# RUN Rscript -e "install.packages(c('agricolae', 'BH', 'BiocManager', 'cowplot', 'devtools', 'doSNOW', 'ggcorrplot', 'ggThemeAssist',\
#     'githubinstall', 'imputeMissings', 'mice', 'minpack.lm', 'missForest', 'mlbench multcomp',\
#     'openxlsx', 'pacman', 'ranger', 'remotes', 'reshape', 'reshape2', 'randomForest', 'rJava', 'rsvg',\
#     'rvg', 'sets', 'sgof', 'tidyverse', 'VIM', 'writexl', 'xlsx', 'XLConnect'))"
# RUN install2.r --error --skipinstalled\
#     agricolae BH BiocManager cowplot devtools doSNOW ggcorrplot ggThemeAssist\
#     githubinstall imputeMissings mice minpack.lm missForest mlbench multcomp \
#     openxlsx pacman ranger remotes reshape reshape2 randomForest rJava rsvg\
#     rvg sets sgof tidyverse VIM writexl xlsx XLConnect
# RUN Rscript -e "BiocManager::install(update = TRUE, ask=FALSE, Ncpus=2)"
# RUN Rscript -e 'BiocManager::install("airway")'
# RUN Rscript -e 'BiocManager::install("aLFQ")'
# RUN Rscript -e 'BiocManager::install("BaylorEdPsych")'
# RUN Rscript -e 'BiocManager::install("biomaRt")'
# RUN Rscript -e 'BiocManager::install("ComplexHeatmap")'
# RUN Rscript -e 'BiocManager::install("DEP")'
# RUN Rscript -e 'BiocManager::install("DESeq")'
# RUN Rscript -e 'BiocManager::install("DESeq2")'
# RUN Rscript -e 'BiocManager::install("EnhancedVolcano")'
# RUN Rscript -e 'BiocManager::install("genefilter")'
# RUN Rscript -e 'BiocManager::install("gmm")'
# RUN Rscript -e 'BiocManager::install("GO.db")'
# RUN Rscript -e 'BiocManager::install("gplots")'
# RUN Rscript -e 'BiocManager::install("imsbInfer")'
# RUN Rscript -e 'BiocManager::install("loadTransitonsMSExperiment")'
# # RUN Rscript -e 'BiocManager::install("limma")'                     # DEP
# RUN Rscript -e 'BiocManager::install("mouse4302.db")'
# RUN Rscript -e 'BiocManager::install("MSstats")'
# RUN Rscript -e 'BiocManager::install("mzR")'
# RUN Rscript -e 'BiocManager::install("org.Hs.eg.db")'
# RUN Rscript -e 'BiocManager::install("org.Mm.eg.db")'
# RUN Rscript -e 'BiocManager::install("PANTHER.db")'
# RUN Rscript -e 'BiocManager::install("PECA")'
# RUN Rscript -e 'BiocManager::install("RCyjs")'
# RUN Rscript -e 'BiocManager::install("readinteger_binary")'
# # RUN Rscript -e 'BiocManager::install("SummarizedExperiment")'      # DEP
# RUN Rscript -e 'BiocManager::install("SWATH2stats")'

# set global options
COPY --chown=rstudio:rstudio . /home/rstudio/