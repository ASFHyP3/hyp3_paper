# Paper Outline

## Outline
- Summary
- Statement of need
    - There is too much satellite imagery for anybody to use
    - Most SAR data require some pre-processing before they are analysis-ready
    - SAR is computationally-intensive and requires complicated/expensive software
    - Related work
- HyP3 description
    - HyP3 development history
        - Started as a student project at UAF
        - Value was evident, so was turned into a full-fledged application
            - Added automated testing, CI/CD, IaC
    - HyP3 Architecture 
        - Architecture diagram
        - Cloud native (AWS) API-based processing workflow for satellite imagery (focus on SAR)
        - Emphasis on high throughput, scalable and cost-effective computing, not high performance computing
        - Designed to work with any image processing pipeline via use of containerized batch jobs for processing
        - API Gateway, Lambda, Dynamo DB, Step Functions, Batch, S3, Docker/Container, ECR, CloudWatch, CloudFormation
            - API Gateway that receives GET, POST requests
            - Post Request logged in DynamoDB NoSQL database
            - Lambda runs on a schedule and watches DynamoDB jobs table for new jobs
            - AWS Step Functions defines workflow for a particular job type
                - Selects appropriate plugin container and memory requirements for job type, watching for failures, logging, and automatically retrying
                - Uploads completed jobs and updates DynamoDB table with job status (FAILED, SUCCEEDED)
            - AWS Batch runs appropriate plugin container for job type
                - UTILIZES SPOT INSTANCES FOR COST MANAGEMENT
                - Scales according to usage compared to monthly budget allowance
            - Results are uploaded to public S3 bucket for download (mention lifecycle?)
    - HyP3 Access
        - HyP3 API
          - Swagger UI with OpenAPI specification
          - Can submit and monitor jobs
        - HyP3-SDK
          - Programmatic Python interface to HyP3 API
          - Can submit, monitor, and download jobs
        - Vertex Integration
          - GUI front-end that allows people to submit RTC jobs, and monitor and download all types of jobs
          - Provides tools for selecting pairs and stacks for InSAR analysis
    - Plugin development via HyP3-cookiecutter
        - Template for creating HyP3 containerized plugins
- Projects utilizing HyP3
    - HyP3-gamma # JS - Might end up combined/closely tied with DockerizedTopsApp? How much will we discuss test-only plugins?
    - DockerizedTopsApp
    - HyP3-autorift
    - Watermap
- Contributors
- Acknowledgments

## Resources
[HyP3 architecture simplified](https://docs.google.com/document/d/1HcSmjMB9YSBgyqb6WBZpu0euvIrzLlzLuCOI1cssGA0/edit)
