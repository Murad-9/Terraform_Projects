# WordPress Deployment with Terraform

## Overview
This project deploys a WordPress website on an AWS EC2 instance using Terraform.

## Infrastructure
- AWS EC2
- Security Group
- Apache
- PHP
- MariaDB
- WordPress

## Terraform Files
- main.tf – AWS resources
- variables.tf – input variables
- terraform.tfvars – variable values
- outputs.tf – deployment outputs
- userdata.sh – WordPress installation script

## Deployment
terraform init
terraform plan
terraform apply

## Result
WordPress is successfully deployed and accessible through the EC2 public IP.
