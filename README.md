# terraform-aws-bhumi-test-VPC

This is complete config to work with this module.

Overview
This Terraform module is designed to create an AWS VPC with a specified CIDR block. It also provisions multiple subnets, both public and private. Additionally, for public subnets, the module sets up an Internet Gateway (IGW) along with the necessary route tables.

Features
Creates a VPC with a specified CIDR block
Configures both public and private subnets
Deploys an Internet Gateway (IGW) for public subnets
Sets up route tables to enable connectivity for public subnets

USAGE

provider "aws" {
  region = "eu-north-1"
}

module "vpc" {
  source = "./module/vpc"

  vpc_config = {
    cidr_block = "10.0.0.0/16"
    name       = "my-test-vpc"
  }
  subnet_config = {
    #key={cidr, az}
    public_subnet-1 = {
      cidr_block = "10.0.0.0/24"
      az         = "eu-north-1a"
      public     = true
    }
    public_subnet-2 = {
      cidr_block = "10.0.2.0/24"
      az         = "eu-north-1a"
      public     = true
    }

    private_subnet = {
      cidr_block = "10.0.1.0/24"
      az         = "eu-north-1b"
    }
  }
}
