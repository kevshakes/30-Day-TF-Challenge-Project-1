# Static Website Hosting with AWS S3 and CloudFront

## Project Overview

This project uses Terraform to set up a static website hosting infrastructure on AWS, utilizing S3 for storage and CloudFront for content delivery. The infrastructure is designed to be scalable, secure, and easy to manage.

## Architecture

- **S3**: Hosts the static website files
- **CloudFront**: Serves as a CDN, providing low-latency access to the website globally
- **Route53** (optional): Manages DNS
- **ACM** (optional): Provides SSL/TLS certificate for HTTPS

## Prerequisites

- AWS Account
- Terraform (version 0.12+)
- AWS CLI configured with appropriate credentials
- Git (for version control)

## Project Structure
```
project-root/
├── modules/
│ └── s3-static-website/
│ ├── main.tf
│ ├── variables.tf
│ └── outputs.tf
├── envs/
│ └── dev/
│ ├── main.tf
│ ├── variables.tf
│ └── terraform.tfvars
├── backend/
│ ├── main.tf
│ ├── variables.tf
│ └── outputs.tf
├── website_files/
│ ├── index.html
│ ├── Other Files
├── backend.tf
├── provider.tf
├── variables.tf
└── README.md
```


## Setup and Deployment

1. **Backend Infrastructure**
   Navigate to the `backend/` directory and run:

```
terraform validate
```
```
terraform init
```
```
terraform apply
```

This sets up the S3 bucket and DynamoDB table for Terraform state management.

2. **Main Project**
From the project root:

terraform validate
terraform init
terraform apply

3. **Website Deployment**
Place your website files in the `website_files/` directory, then run:


terraform apply in the `envs/dev/` directory.

## Modules

### S3 Static Website

This module creates an S3 bucket configured for static website hosting and fronted using Amazon Cloudfront.

**Inputs:**
- `bucket_name`: Name of the S3 bucket (must be globally unique)

**Outputs:**
- `website_endpoint`: The website endpoint for the S3 bucket
- `bucket_name`: The name of the created S3 bucket

## Environments

### Dev

The `envs/dev/` directory contains the configuration for the development environment. Customize `terraform.tfvars` for environment-specific variables.

## State Management

This project uses an S3 backend with DynamoDB for state locking, ensuring safe concurrent operations and state versioning.

## Security Considerations

- S3 bucket is configured with appropriate public access settings
- CloudFront is set up to use HTTPS only
- IAM policies follow the principle of least privilege

## Customization

- Modify `variables.tf` files to add or change input variables
- Adjust CloudFront settings in `envs/dev/main.tf` for caching behavior
- Add additional resources as needed in the respective `main.tf` files

## Troubleshooting

- Ensure AWS CLI is properly configured
- Check IAM permissions if encountering access denied errors
- Verify that S3 bucket names are globally unique

## Contributing

Please read CONTRIBUTING.md for details on our code of conduct and the process for submitting pull requests.

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.

## Acknowledgments

- AWS Documentation
- Terraform Documentation
- Contributors and maintainers of this project
