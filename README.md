# Boto3
Dealing with AWS Infra with python scripts

---

# EC2 Instance Inventory Script

## Overview

This Python script interacts with the AWS EC2 service to gather details about running EC2 instances across multiple regions. It collects essential information for each running instance and stores it in a pandas DataFrame. You can optionally export the results to a CSV file for further analysis or reporting.

## Features

- Queries EC2 instances across multiple AWS regions.
- Retrieves key information such as:
  - Instance ID
  - Instance Name (from the "Name" tag, if available)
  - Instance Type
  - Lifecycle (On-demand or Spot)
  - Availability Zone
  - AMI ID
  - AMI Name
- Option to export the data to a CSV file (`instances_list.csv`).

## Prerequisites

### Python Dependencies

Ensure you have Python 3.x and the necessary libraries installed. You can install the required libraries with pip:

```bash
pip install boto3 pandas
```

### AWS Credentials

This script requires AWS credentials to access the EC2 instances. You can configure your AWS credentials using one of the following methods:

1. **AWS CLI**: If you have the AWS CLI installed, configure your credentials by running:

    ```bash
    aws configure
    ```

2. **Environment Variables**: Set your AWS credentials in the environment:

    ```bash
    export AWS_ACCESS_KEY_ID="your-access-key-id"
    export AWS_SECRET_ACCESS_KEY="your-secret-access-key"
    ```

3. **IAM Role**: If running on an EC2 instance with an IAM role, the credentials will automatically be assumed.

## Supported Regions

The script fetches EC2 instance details from the following AWS regions:

- **US**: us-east-1, us-east-2, us-west-1, us-west-2
- **Asia Pacific**: ap-south-1, ap-northeast-1, ap-northeast-2, ap-northeast-3, ap-southeast-1, ap-southeast-2
- **Canada**: ca-central-1
- **Europe**: eu-central-1, eu-west-1, eu-west-2, eu-west-3, eu-north-1
- **South America**: sa-east-1

## How It Works

1. **Regions List**: The script iterates through a predefined list of AWS regions.
2. **EC2 Client**: For each region, it initializes an EC2 client using `boto3`.
3. **Describe Instances**: The script retrieves details about EC2 instances in each region using `describe_instances`.
4. **Instance Data**: For each running instance, it collects:
   - Instance ID
   - Instance Type
   - Availability Zone
   - Lifecycle (On-demand or Spot)
   - AMI ID and AMI Name (from the image)
5. **Name Tag**: It checks the instance's tags for the "Name" tag and uses that as the instance's name.
6. **AMI Information**: For each instance, it fetches additional details about the AMI (Amazon Machine Image) using `describe_images`.
7. **Data Compilation**: The results are stored in a pandas DataFrame for easy analysis.
8. **Exporting to CSV**: You can optionally save the results to a CSV file (`instances_list.csv`).

## How to Run

1. Clone or download this repository.
2. Install the required dependencies:

    ```bash
    pip install boto3 pandas
    ```

3. Make sure your AWS credentials are configured (as mentioned in the prerequisites).
4. Run the script:

    ```bash
    python fetch_instances.py
    ```

5. The script will print a DataFrame with the details of the running EC2 instances across all specified regions and save the data to `instances_list.csv`.

## Example Output

When you run the script, it will display a DataFrame similar to the following:

| Region      | Availability Zone | Instance Name | Instance ID | Instance Type | Lifecycle | AMI ID       | AMI Name      |
|-------------|-------------------|---------------|-------------|---------------|-----------|-------------|---------------|
| us-east-1   | us-east-1a         | MyInstance    | i-1234567890 | t2.micro      | On-demand | ami-12345678 | Amazon Linux 2|
| eu-west-1   | eu-west-1b         | WebServer     | i-0987654321 | t3.medium     | Spot      | ami-87654321 | Ubuntu 20.04  |

## Saving to CSV

The script saves the results as `instances_list.csv` in the same directory as the script. You can open this file with any spreadsheet tool for further analysis.

## Contributing

Feel free to submit issues or pull requests if you'd like to contribute to this repository!

---

