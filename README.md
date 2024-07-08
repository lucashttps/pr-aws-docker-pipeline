# Docker Image Pipeline with AWS and GitHub Actions

## Overview
This repository contains a GitHub Actions workflow for building, tagging, and pushing Docker images to Amazon Elastic Container Registry (ECR) whenever a pull request (PR) is opened or merged. It also includes steps to delete the Docker image when the PR is closed.

## Workflow Description

### Events
- **on: pull_request**
  - Types: `opened`, `merged`, `closed`

### Jobs
1. **opened**
   - Triggered when a PR is opened or merged, but not closed, and the branch starts with `release/`.
   - **Steps:**
     1. **AWS Login**: Configures AWS credentials using the GitHub Secrets.
     2. **Docker Login**: Logs into the Docker registry using AWS ECR.
     3. **Checkout Code**: Checks out the repository code.
     4. **Build, Tag, and Push Docker Image**: Builds the Docker image, tags it, and pushes it to the specified Amazon ECR repository.
     5. **Comment on PR**: Comments on the PR with the Docker image pull command.

2. **closed**
   - Triggered when a PR is closed and the branch starts with `release/`.
   - **Steps:**
     1. **AWS Login**: Configures AWS credentials using the GitHub Secrets.
     2. **Docker Login**: Logs into the Docker registry using AWS ECR.
     3. **Checkout Code**: Checks out the repository code.
     4. **Delete Docker Image**: Deletes the Docker image from Amazon ECR.
     5. **Comment on PR**: Comments on the PR indicating the Docker image has been deleted.

## Workflow Configuration
### Workflow File: `.github/workflows/docker-image-pipeline.yml`