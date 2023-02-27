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
HyP3 is a cloud processing pipeline that is designed with a serverless architecture and to follow AWS architecture best practices. It also strives to make a clear separation between the plugins that perform the image processing and the pipeline in which this task is performed. See Figure FF for the AWS architecture diagram.

Users can interact with HyP3 via three access methods, a graphical interface that is integrated within ASF's data search platform (Vertex), a Python software development kit (SDK), or directly via an application program interface (API). The API follows the OpenAPI specification and provides GET/POST requests for submitting job requests to HyP3, checking user information, and for checking the status of previously requested jobs. Both the SDK and graphical interface translate their inputs into API call. The API is maintained by an API Gateway (Figure FF), and all submitted jobs are stored within a DynamoDB NoSQL database.

An EventBridge cron event is set to occur every XX seconds, and this event triggers a Lambda that checks the DynamoDB jobs table for newly submitted jobs. If new jobs are present, the Lambda submits these jobs to an AWS Step Functions. Similar to what is possible in Apache Airflow, Step Functions defines a state machine that can be used to execute the processing workflow for a particular job.

The workflow begins by inspecting the job definition for the job type. This job type will be used to determine which image processing workflow is run and what computing resources the job needs. With this setup, a HyP3 deployment can contain an arbitrary number of different image processing workflows. Once the memory and compute resources requirements are determined, the workflow submits the job processing via AWS Batch, which handles the scheduling of the execution and the management of resources. For HyP3, we use the AWS Elastic Container Service (ECS) inside of Batch to run the image processing workflows within Docker containers that are unique to each job type. Upon successful processing, the job results are uploaded to S3. The encapsulation of all processing-specific code within Docker containers with a simple interface is an important piece of the HyP3 architecture and is discussed in further detail in the Workflow Containers section below. All processing workflows are run on EC2-spot instance to reduce the cost of image processing.

After the processing step is complete, Step Functions check if the jobs was successful. If not, the job is re-submitted up to three times in order to ensure that the job did not fail due to a reclaiming of spot resources by AWS. Then, if the final run was successful the job entry in the DynamoDB table is updated so that the job status is "success" and records the location of the output image products in S3. If the final run wasn't successful, the job entry in the DynamoDB table is updated so that the job status is "failed" and the log of the last failed job is uploaded to s3 and the log location is recorded in the table.



# Citations

TO DO 

# Figures

TO DO 

# Acknowledgments

TO DO 

# References

TO DO
