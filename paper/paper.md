---
title: 'HyP3'
tags:
  - Python
  - astronomy
  - dynamics
  - galactic dynamics
  - milky way
authors:
  - name: Adrian M. Price-Whelan
    orcid: 0000-0000-0000-0000
    equal-contrib: true
    affiliation: "1, 2" # (Multiple affiliations must be quoted)
  - name: Author Without ORCID
    equal-contrib: true # (This is how you can denote equal contributions between multiple authors)
    affiliation: 2
  - name: Author with no affiliation
    corresponding: true # (This is how to denote the corresponding author)
    affiliation: 3
affiliations:
  - name: Lyman Spitzer, Jr. Fellow, Princeton University, USA
    index: 1
  - name: Institution Name, Country
    index: 2
  - name: Independent Researcher, Country
    index: 3
date: 13 August 2017
bibliography: paper.bib
# CURRENTLY THIS IS JUST THE SAMPLE OUTLINE DIRECTLY FROM
  # https://joss.readthedocs.io/en/latest/submitting.html#example-paper-and-bibliography
---

# Summary

TO DO

# Statement of need

TO DO

# HyP3 Description

## Development History
HyP3 grew out of a need for a standardized pipeline to perform image processing workflows at the Alaska Satellite Facility (ASF) Distributed Active Archive Center (DAAC). HyP3 was initially created by a group of University of Alaska Fairbanks students in 2017 who were interning at ASF. These students created a prototype version of HyP3 that was designed to handle workflows that ran on-premise and in the AWS cloud. This prototype was iterated upon for several more years, and by 2019 it was capable of performing many SAR-specifc image processing workflows.

By 2019 however, it was clear that re-designing HyP3 to take advantage of evolving technologies (namely the new AWS Batch service, infrastructure-as-code, and containerized workflows) would greatly improve its utility. Thus in 2019 HyP3 was re-designed to exist entirely within the AWS cloud and to encapsulate application-specific processing workflows within Docker containers. The re-design was completed in 2020, and on-demand SAR image processing services that utilized HyP3 (including RTC and InSAR processing) were made available to the public for free via an API, Python SDK, and ASF's data search website.

Throughout 2020-2022 new image processing services were added to HyP3 including a glacier velocity tracking, and flood inundation mapping workflows and the user base grew to XX users producing XX image products on average every month. Since 2021, many groups have recognized the utility of HyP3. In 2022 HyP3 was deployed within NASA's Earthdata Cloud and many other deployments of HyP3 now exist at other institutions (see the Ongoing Projects section for details).

## HyP3 Architecture


# Citations

TO DO 

# Figures

TO DO 

# Acknowledgments

TO DO 

# References

TO DO
