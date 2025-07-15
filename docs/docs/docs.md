# CloudTAK Documentation

Welcome to the official documentation for [CloudTAK](https://github.com/dfpc-coe/CloudTAK), a full-featured in-browser TAK client powered by AWS that facilitates ETL operations to bring non-TAK data sources into a TAK Server.

CloudTAK provides a comprehensive suite of tools for managing geospatial data, conducting operations, and integrating with various data sources in support of situational awareness and emergency response activities.

## Getting Started

This documentation is organized into three main sections to help you get started with CloudTAK:

### 🚀 Deploy

Learn how to deploy and configure CloudTAK in your environment:

- **Local Development**: Set up CloudTAK locally using Docker Compose for development and testing
- **AWS Deployment**: Deploy CloudTAK to AWS using the provided CloudFormation templates
- **Prerequisites**: Required AWS services and dependencies
- **Configuration**: Environment variables, database setup, and administrative settings
- **Infrastructure**: VPC, ECS, ECR, and other AWS resource requirements

Whether you're running a quick local test or deploying a production instance on AWS, the Deploy section will guide you through the complete setup process.

### 🛠️ Develop

Extend and customize CloudTAK for your specific needs:

- **Local Development Setup**: Configure your development environment
- **ETL Tasks**: Create custom Lambda tasks to ingest data from external sources
- **API Reference**: Comprehensive guide to CloudTAK's REST API
- **Task Development**: Build and deploy ETL tasks using Docker and AWS Lambda
- **Data Integration**: Convert various data formats to GeoJSON or CoT XML
- **Contributing**: Guidelines for contributing to the CloudTAK project

The Develop section provides everything developers need to build custom integrations and extend CloudTAK's functionality.

### 📚 User Guide

Master the CloudTAK interface and features:

- **Web Interface**: Navigate the in-browser TAK client
- **Data Management**: Import, export, and manage geospatial data
- **Mission Planning**: Create and manage missions and operations
- **Layer Management**: Work with map layers and data sources
- **User Administration**: Manage users, groups, and permissions
- **ETL Operations**: Configure and monitor data ingestion tasks

The User Guide helps operators and administrators effectively use CloudTAK for their operational needs.

## About CloudTAK

CloudTAK combines the power of cloud computing with the Team Awareness Kit (TAK) ecosystem to provide:

- **Real-time Situational Awareness**: Live data feeds and collaborative mapping
- **Data Integration**: ETL capabilities to incorporate diverse data sources
- **Scalable Architecture**: Cloud-native design built for AWS
- **Browser-based Access**: No client installation required
- **Mission Support**: Tools for planning and conducting operations

For technical details, source code, and the latest updates, visit the [CloudTAK repository](https://github.com/dfpc-coe/CloudTAK) on GitHub.

---

*Ready to get started? Choose one of the sections above based on your role and objectives.*
