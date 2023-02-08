# Paper Outline

## Outline
- Summary
- Statement of need
    - There is too much satellite imagery for anybody to use
    - Related work
- HyP3 description
    - HyP3 development history
        - Started as a student project at UAF
        - Value was evident, so was turned into a full-fledged application
            - Added automated testing, CI/CD, IaC
    - HyP3
        - Architecture diagram
        - Cloud native (AWS) API-based processing workflow for satellite imagery (focus on SAR)
        - API Gateway, Lambda, Dynamo DB, Step Functions, Batch, S3, Docker/Container, ECR, CloudWatch, CloudFormation
            - API Gateway that receives GET, POST requests
                - Swagger UI using OpenAPI specification
            - Post Request logged in DynamoDB NoSQL database
            - Lambda runs on a schedule and watches DynamoDB jobs table for new jobs
            - AWS Step Functions defines workflow for a particular job type
                - Involves steps such as selecting appropriate plugin container for job type, watching for failures, logging, uploading of completed jobs, updating DynamoDB table, automatic retries
            - AWS Batch runs appropriate plugin container for job type
                - UTILIZES SPOT INSTANCES FOR COST MANAGEMENT
            - Results are uploaded to public S3 bucket for download
        - Emphasis on high throughput, scalable and cost-effective computing, not high performance computing
        - Designed to work with any image processing pipeline via use of containerized batch jobs for processing
    - HyP3 API
    - HyP3-SDK
        - Programmatic Python interface to HyP3 API
        - Can submit, monitor, and download jobs
    - Vertex Integration
        - GUI front-end that allows people to submit, monitor, and download jobs
    - HyP3-cookiecutter
        - Template for creating HyP3 containerized plugins
- Projects utilizing HyP3
    - HyP3-gamma
    - HyP3-autorift
    - DockerizedTopsApp
    - Watermap
- Contributors
- Acknowledgment

## Resources
[HyP3 architecture simplified](https://docs.google.com/document/d/1HcSmjMB9YSBgyqb6WBZpu0euvIrzLlzLuCOI1cssGA0/edit)
