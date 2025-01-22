# GitHub Actions Workflow for Reqres Service API

This GitHub Actions workflow is a template that will be triggered on `push`, meaning it runs every time code is pushed to the repository. It will configure and deploy the Reqres service API.

## Environment Variables

The workflow sets up several environment variables, including:
- `KONG_KONNECT_TOKEN`
- `KONG_CP_NAME`
- `SERVICE_NAME`
- `TAG_NAME`

These variables are used throughout the workflow.

## Workflow Overview

The workflow consists of a single job, `deploy-my-demo-api`, which runs on the latest version of Ubuntu. This job has several steps:

### 1. Setup Deck
This step uses the `kong/setup-deck@v1` action to set up Deck, a command-line tool for Kong Gateway. The version of Deck being used is specified as `1.29.2`.

### 2. Clone Repository
This step uses the `actions/checkout@v2` action to clone the repository into the runner, allowing the workflow to access its contents.

### 3. Convert OpenAPI to Kong Format
This step creates a directory named `generated` and then uses Deck to convert an OpenAPI specification file to a Kong format file. It also adds tags to the services in the generated file.

### 4. Add Global Plugins and Route Plugins to the Generated File
This step uses Deck to add global plugins and route plugins to the generated file.

### 5. Validate Generated File
This step uses Deck to validate the generated file, ensuring it is correctly formatted and contains no errors.

### 6. Diff Generated File
This step uses Deck to compare the generated file with the current configuration on the Kong control plane. It uses the `diff` command to show any differences.

### 7. Sync Generated File
This step uses Deck to synchronize the generated file with the Kong control plane, applying any changes found in the diff step.

## Notes

The commented-out section of code appears to be a previous version of the workflow that included a step to backup the old service configuration. This step is not currently being used.

## Summary

Overall, this workflow automates the process of converting an OpenAPI specification to a Kong format, adding plugins, validating the file, and synchronizing it with the Kong control plane.
