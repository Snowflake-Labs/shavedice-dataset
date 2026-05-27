# Snowflake Cyclic VM Demand Dataset

This repository contains documentation for the dataset that accompanies our
[ICPE 2025](https://icpe2025.spec.org/) paper, "Shaved Ice: Optimal Compute Resource Commitments for
Dynamic Multi-Cloud Workloads".  It also includes example [R](http://www.r-project.org) and Python notebooks to
read and visualize the data, including scripts to reproduce the
figures and analysis results in the paper.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15015992.svg)](https://doi.org/10.5281/zenodo.15015992)

This project is archived on [Zenodo](https://zenodo.org/), an open-access repository, to ensure long-term reproducibility of the research.

## Dataset

The dataset contains normalized and obfuscated hourly data about VM demand in four example Snowflake deployments over a period of 3 years from 2/1/2021 to 1/30/2024.
Each hour includes (type of VM, region, number of VMs of that type) used at that time.
This dataset is available in both [compressed CSV](./hourly_normalized.csv.gz) and [Parquet](./hourly_normalized.parquet) formats.

### Schema

* *Timestamp*: An hourly timestamp for the record.
* *VM Type*: This field is obfuscated with the precise VM identifier from the Cloud Service Provider mapped into a capital letter.
* *Region*: The region where the VM was deployed.  This field is obfuscated with the precise region name from the Cloud Service Provider mapped into a number between 1 and 4.
* *Count*: The number of VMs of the specified type, region, and hour.  This field is normalized such that the largest type, region, hour tuple is set to 1000 in each region and other values are scaled linearly to the nearest whole number.

### Related Datasets

The [Snowset dataset](https://github.com/resource-disaggregation/snowset) provides information about 70 million queries run on Snowflake in 2018 to accompany the paper "Building an Elastic Query Engine on Disaggregated Storage" by Vuppalapati, et al.

This earlier data set shows the clear diurnal and weekly patterns of Snowflake workloads, particularly for read-only ad-hoc and OLAP queries.
It also provides detailed statistics collected from each of the 70 million queries.
However, this trace covers only 2 weeks of time and so is not sufficient for analysis of longer-term strategies to purchase commitments and optimize cloud compute spending. 

## Scripts

The [figures](./figures/) directory has some scripts to reproduce the figures and analysis in the paper.

* *[IntroAnalysis.Rmd](IntroAnalysis.Rmd)*: Simple reading and visualization of the dataset in R ([pdf notebook](IntroAnalysis.pdf)).

![VM Demand Timeseries](timeseries.png)

* *[IntroAnalysis-py.ipynb](IntroAnalysis-py.ipynb)*: Simple reading and visualization of the dataset in Python.

* *[figures/timeseries.Rmd](figures/timeseries.Rmd)*: Snowflake Workload Analysis ([pdf notebook](figures/timeseries.pdf))

![Daily Workload Pattern](figures/dailypattern.png)
![Holiday Effect](figures/annualholiday.png)

* *[figures/Optimization.Rmd](figures/optimization.Rmd)*: Visualization and optimization of minimum-cost savings plan levels. ([pdf notebook](figures/optimization.pdf))

![Commitment Level Optimization](figures/3x3.png)

* *[animation/optimization.Rmd](animation/optimization.Rmd)*: Animation of the optimization process ([pdf notebook](animation/optimization.pdf))

![Optimization Animation](animation/combined.mp4)

## Privacy Concerns

There are no identifiers in the dataset that could potentially reveal
a customer's identity.  Public access to the information in this dataset
does not lead to any privacy or other ethical concerns.

This data represents a subset of Snowflake VM demand from select regions.
Therefore, neither the overall growth rates nor the total demand of Snowflake
VMs can be inferred.

## Papers Using This Dataset

- Hector Pena and Steven Cheun. "[Weekly Seasonality in Cloud Demand: Lessons from Snowflake's Shaved Ice Dataset](https://dl.acm.org/doi/abs/10.1145/3777911.3800696)." ICPE Companion '26, Florence, Italy, 2026.

## Contact

Murray Stokely (murray.stokely@snowflake.com)

## Usage

Copyright 2025 Snowflake Inc. This data is licensed under CC BY 4.0.
To view a copy of this license, visit https://creativecommons.org/licenses/by/4.0/

Kindly cite the following publication if you are using our dataset:

```
@inproceedings {snowflake-icpe25,
  author = {Murray Stokely and Neel Nadgir and Jack Peele and Orestis Kostakis},
  title = {Shaved Ice: Optimal Compute Resource Commitments for Dynamic Multi-Cloud Workloads},
  booktitle = {Proceedings of the 16th ACM/SPEC International Conference on Performance Engineering (ICPE '25)},
  year = {2025},
  publisher = {Association for Computing Machinery},
  address = {New York, NY, USA},
  url = {https://doi.org/10.1145/3676151.3719353},
  doi = {10.1145/3676151.3719353}
}
```