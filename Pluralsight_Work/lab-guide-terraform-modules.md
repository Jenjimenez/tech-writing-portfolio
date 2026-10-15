---
last_updated: 2026-10-14
---
# Lab Guide: Develop and Reuse Terraform Modules

<div class="case-summary">
  <dl>
    <div><dt>The challenge</dt><dd>The lab builds in stages, from a public module to event notifications to a custom, versioned module. A single wrong value or an outdated expected output early on can break every step that follows.</dd></div>
    <div><dt>My contribution</dt><dd>Reviewed, tested, and revised the lab guide: ran each step in the lab environment, checked each Terraform configuration, and edited the instructions for clarity and consistency.</dd></div>
    <div><dt>The result</dt><dd>A published lab where each stage ends with a checkpoint, so learners can confirm their work before moving on.</dd></div>
    <div><dt>Audience</dt><dd>Learners practicing infrastructure as code in a Pluralsight hands-on cloud lab.</dd></div>
    <div><dt>The sample</dt><dd>The full lab guide, below. <a href="https://www.pluralsight.com/labs/aws/develop-and-reuse-terraform-modules">View the published lab on Pluralsight</a>.</dd></div>
  </dl>
</div>

<div class="tested-box" id="what-i-tested">
  <p class="tested-title">What I tested</p>
  <ul>
    <li>Ran every step as a learner would, in the lab environment.</li>
    <li>Validated each Terraform configuration before following the steps that depend on it.</li>
    <li>Confirmed that plan and apply output match what the guide tells learners to expect, such as <code>Plan: 4 to add</code>.</li>
    <li>Checked that the Lambda test event and CloudWatch logs show the messages the guide describes.</li>
  </ul>
</div>

## Getting started

### Getting to VS Code

1. On the AWS console home page, click **EC2** to go to the EC2 dashboard.
2. Click **Instances (running)** to show the EC2 instance set up for this lab.
3. Click the instance ID link that begins with `i-`.
4. Copy the **Public IPv4 address**.
5. In a new browser tab, go to the following URL and replace `<public-ipv4-address>` with your copied address:

    ```text
    https://<public-ipv4-address>:8080
    ```

    Your browser displays a security warning because the server uses a self-signed certificate. Continue to the site. You might need to try more than once.
6. When prompted, enter the password provided in the lab credentials in the **Password** field.

The site loads, and VS Code opens in your browser.

### Set up the solution directory

1. In VS Code, click the **Search** bar at the top.
2. Click **Show and Run Commands**.
3. Type `New Terminal`.
4. Click **Terminal: Create New Terminal**.

    This will launch a shell **TERMINAL** at the bottom of VS Code, which is running commands directly on the EC2 instance.

5. In the **TERMINAL**, type the following command and press **Enter** to scaffold a directory structure for your solution files.

    ```bash
    mkdir src && cd src && mkdir terraform && mkdir lambda
    ```

    If a **clipboard** warning appears, click **Allow**.

6. In the left-hand VS Code activity bar, select **Explorer**.
7. Select **Open Folder**, and then select the `src` folder.
8. Click **OK**, and wait for the workspace trust prompt to appear.

    The prompt might take one or two minutes to appear. If an **Error loading webview** notification appears, dismiss it.

    If the workspace trust prompt does not appear, reload the browser tab.
9. Select **Trust the authors of all files in the parent folder "cloud_user"**, and then select **Yes, I trust the authors**.

## Using public modules

### Provision an S3 bucket

1. In the **Explorer**, select the `terraform` folder, and then select **New File**.
2. Name the file `main.tf`, then press **Enter**.
3. Set up the AWS and Random providers by adding the following Terraform configuration:

    ```hcl
    terraform {
      required_providers {
        aws = {
          source  = "hashicorp/aws"
          version = "6.0.0"
        }
        random = {
          source  = "hashicorp/random"
          version = "3.7.2"
        }
      }
    }

    provider "aws" {
      region = "us-east-1"
    }
    ```

4. At the end of `main.tf`, add the following `random_id` resource to create a unique suffix for the S3 bucket name:

    ```hcl
    resource "random_id" "s3_suffix" {
      byte_length = 4
    }
    ```

5. Add the following configuration to provision an S3 bucket by using the public AWS S3 bucket module:

    ```hcl
    data "aws_caller_identity" "current" {}
    data "aws_iam_policy_document" "s3_bucket_access" {
      statement {
        sid    = "AllowEc2RoleReadWrite"
        effect = "Allow"

        principals {
          type        = "AWS"
          identifiers = [data.aws_caller_identity.current.arn]
        }

        actions = [
          "s3:*"
        ]

        resources = [
          module.s3_bucket.s3_bucket_arn,
          "${module.s3_bucket.s3_bucket_arn}/*",
        ]
      }
    }

    module "s3_bucket" {
      source  = "terraform-aws-modules/s3-bucket/aws"
      version = "5.1.0"

      bucket = "ps-tf-bucket-${random_id.s3_suffix.hex}"
      versioning = {
        status     = "Enabled"
        mfa_delete = "Disabled"
      }

      force_destroy = true
      attach_policy = true
      policy        = data.aws_iam_policy_document.s3_bucket_access.json
    }
    ```

    > **Note:** When defining the bucket name, you used the `random_id` resource defined earlier to ensure the bucket name is unique. The hex property of the `random_id` resource gives a hexadecimal value of the id and will always return twice as many characters as the specified byte length. In this example it will be an eight-character suffix.
    > 
    > The `aws_caller_identity` data source identifies the principal running Terraform. The `aws_iam_policy_document` data source creates a bucket policy that allows that principal, which is the EC2 instance in this lab, to read from and write to the S3 bucket.

6. If the **TERMINAL** closed when you opened the `src` folder, open a new terminal: click the **Search** bar, click **Show and Run Commands**, and then click **Terminal: Create New Terminal**.
7. In the **TERMINAL**, run the following command to change to the `terraform` directory:

    ```bash
    cd terraform
    ```

    Then run the following command to initialize Terraform and download the configured providers:

    ```bash
    terraform init
    ```

    You will see output describing, finding, and installing the `hashicorp/random` and `hashicorp/aws` providers. When Terraform is finished initializing, you will see the following message:

    ```text
    Terraform has been successfully initialized!
    ```

8. In the **TERMINAL**, run the following command to preview what actions Terraform will take.

    ```bash
    terraform plan
    ```

    Terraform displays the properties of the resources it will create. A `Deprecated Attribute` warning might appear. You can safely ignore it. 

    The plan ends with the following result:

    ```text
    Plan: 5 to add, 0 to change, 0 to destroy.
    ```

9. Run the following command to provision the resources specified in `main.tf`:

    ```bash
    terraform apply
    ```

10. Terraform will run another `plan` before prompting you with `Do you want to perform these actions?`. Enter `yes` and Terraform will begin provisioning the resources.

    Once the resources are provisioned, you will see a message saying:

    ```text
    Apply complete! Resources: 5 added, 0 changed, 0 destroyed.
    ```

11. Go to the browser tab that contains the AWS console **EC2** page.
12. In the search bar, type `S3`, and then select **S3**.
13. Verify that the bucket name begins with `ps-tf-bucket-` and ends with the random eight-character suffix.
14. Return to VS Code.

### Provision a Lambda function

1. In the **Explorer** on the left, click the `lambda` folder, and then click **New File**.
2. Name the file `handler.py`.
3. Add the following handler code:

    ```python
    def lambda_handler(event, context):
        print("Received S3 Bucket Notification")
        print(event)
    ```

4. Go back to `main.tf`, and add the following Terraform configuration to provision a Lambda function:

    ```hcl
    data "aws_iam_policy_document" "assume_role" {
      statement {
        effect = "Allow"

        principals {
          type        = "Service"
          identifiers = ["lambda.amazonaws.com"]
        }

        actions = ["sts:AssumeRole"]
      }
    }

    resource "aws_iam_role" "lambda_role" {
      name               = "lambda_execution_role"
      assume_role_policy = data.aws_iam_policy_document.assume_role.json
    }

    resource "aws_iam_role_policy_attachment" "attach-basic-execution" {
      role       = aws_iam_role.lambda_role.name
      policy_arn = "arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole"
    }

    data "archive_file" "function" {
      type        = "zip"
      source_file = "../lambda/handler.py"
      output_path = "../lambda/function.zip"
    }

    resource "aws_lambda_function" "s3_handler" {
      filename         = data.archive_file.function.output_path
      function_name    = "s3_handler_lambda_function"
      role             = aws_iam_role.lambda_role.arn
      handler          = "handler.lambda_handler"
      source_code_hash = data.archive_file.function.output_base64sha256

      runtime = "python3.12"
    }

    resource "aws_cloudwatch_log_group" "lambda_group" {
      name = "/aws/lambda/${aws_lambda_function.s3_handler.function_name}"
    }
    ```

    > **Note:** This configuration creates the IAM role and policy attachment required by the Lambda function, packages `handler.py` in a `.zip` file, provisions the Lambda function, and creates a CloudWatch log group for the function.

5. In the **TERMINAL**, run the following command to install the Archive provider:

    ```bash
    terraform init -upgrade
    ```

6. Run the following command:

    ```bash
    terraform apply
    ```

    Terraform displays the plan first. At the end of the plan output, you should see:

    ```text
    Plan: 4 to add, 0 to change, 0 to destroy.
    ```

7. When prompted with `Do you want to perform these actions?`, enter `yes`, and Terraform will begin provisioning the resources. A `Deprecated Attribute` warning might appear. You can safely ignore it.

    Once the resources are provisioned, you will see a message saying:

    ```text
    Apply complete! Resources: 4 added, 0 changed, 0 destroyed.
    ```

8. Return to the AWS Console.
9. In the search bar, type `Lambda`, and then select **Lambda**.
10. Select **s3_handler_lambda_function**.
11. Verify the `handler.py` file shows in the file explorer, and the code matches what you created earlier.
12. Click the **Test** tab.
13. Click **Create new test event**.
14. Click **Invoke** to send a **hello-world** test event to your Lambda.

    Between the `START RequestId` and `END RequestId` entries, verify that the output includes:

    ```text
    Received S3 Bucket Notification
    {'key1': 'value1', 'key2': 'value2', 'key3': 'value3'}
    ```

### Provision an S3 notification

1. Return to VS Code.
2. In `main.tf`, add the following Terraform configuration to allow the S3 bucket to invoke the Lambda function:

    ```hcl
    resource "aws_lambda_permission" "allow_bucket" {
      statement_id  = "AllowExecutionFromS3Bucket"
      action        = "lambda:InvokeFunction"
      function_name = aws_lambda_function.s3_handler.arn
      principal     = "s3.amazonaws.com"
      source_arn    = module.s3_bucket.s3_bucket_arn
    }
    ```

3. Add the following S3 bucket notification resource:

    ```hcl
    resource "aws_s3_bucket_notification" "bucket_notification" {
      bucket = module.s3_bucket.s3_bucket_id

      lambda_function {
        lambda_function_arn = aws_lambda_function.s3_handler.arn
        events              = ["s3:ObjectCreated:*"]
      }

      depends_on = [aws_lambda_permission.allow_bucket]
    }
    ```

4. In the **TERMINAL**, run the following command to provision the resources without a confirmation prompt:

    ```bash
    terraform apply --auto-approve
    ```

    Terraform displays the plan and, because of the `--auto-approve` flag, immediately begins provisioning the resources.

    When the operation finishes, Terraform displays:

    ```text
    Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
    ```

5. Return to the AWS Lambda console page for **s3_handler_lambda_function**.
6. Reload the browser tab, and verify the **S3** trigger appears.
7. Click the **S3** trigger.
8. On the **Configuration** tab, select the bucket name that begins with `ps-tf-bucket-`.
9. Copy the full bucket name.
10. Return to the VS Code **TERMINAL**, and enter the following command to save your bucket name in an environment variable:

    ```bash
    export BUCKET_NAME=ps-tf-bucket-<random-id>
    ```

    Make sure the command has the full bucket name, for example `ps-tf-bucket-d475529f`, and does not include the placeholder `<random-id>`.

11. Run the following AWS CLI command to copy a file to S3 and trigger the Lambda:

    ```bash
    aws s3 cp ../lambda/handler.py s3://$BUCKET_NAME
    ```

12. Return to the AWS Console **ps-tf-bucket-** page.
13. Click the **Refresh Objects** icon, and verify the `handler.py` file is uploaded.
14. Return to the Lambda console page for **s3_handler_lambda_function**.
15. Select the **Monitor** tab and verify that the **Invocations** graph shows an invocation.
16. Click **View CloudWatch logs**. The function's logs open in a new browser tab.
17. Click the most recent **Log stream** with the following format: `YYYY/MM/DD/[$LATEST]<random-id>`.
18. Verify that the log contains `Received S3 Bucket Notification` and the S3 notification event.

## Develop a custom Terraform module

### Create an S3 notification module

1. Switch back to the browser tab containing VS Code.
2. In the **EXPLORER** on the left, click the **terraform** folder, and then click the icon for **New Folder...**. Name the folder `modules`.
3. Create another new folder within the **modules** folder called `s3_notification`.
4. Within the **s3_notification** folder, create two files: `main.tf` and `variables.tf`.
5. Copy the `aws_lambda_permission` and `aws_s3_bucket_notification` resources from your existing `main.tf` file into the new `modules/s3_notification/main.tf` file. Use the following Terraform code for reference:

    ```hcl
    resource "aws_lambda_permission" "allow_bucket" {
      statement_id  = "AllowExecutionFromS3Bucket"
      action        = "lambda:InvokeFunction"
      function_name = aws_lambda_function.s3_handler.arn
      principal     = "s3.amazonaws.com"
      source_arn    = module.s3_bucket.s3_bucket_arn
    }

    resource "aws_s3_bucket_notification" "bucket_notification" {
      bucket = module.s3_bucket.s3_bucket_id

      lambda_function {
        lambda_function_arn = aws_lambda_function.s3_handler.arn
        events              = ["s3:ObjectCreated:*"]
      }

      depends_on = [aws_lambda_permission.allow_bucket]
    }
    ```

6. In `modules/s3_notification/variables.tf`, add the following input variable for the S3 bucket identifiers:

    ```hcl
    variable "bucket" {
      description = "S3 Bucket Identifiers"
      type = object({
        arn = string
        id  = string
      })
    }
    ```

7. At the end of `variables.tf`, add the following input variable for the Lambda notification configuration:

    ```hcl
    variable "lambda_notification" {
      description = "Lambda Function notification configuration object"
      type = object({
        arn           = string
        events        = list(string)
        filter_prefix = optional(string)
        filter_suffix = optional(string)
      })
    }
    ```

8. In `modules/s3_notification/main.tf`, modify the Terraform configuration to use the variables, rather than hard coding the values:

    In the `aws_lambda_permission` resource:

    - Change `function_name = aws_lambda_function.s3_handler.arn` to `function_name = var.lambda_notification.arn`
    - Change `source_arn = module.s3_bucket.s3_bucket_arn` to `source_arn = var.bucket.arn`

    In the `aws_s3_bucket_notification` resource:

    - Change `bucket = module.s3_bucket.s3_bucket_id` to `bucket = var.bucket.id`
    - Replace the `lambda_function` block with the following:

      ```hcl
      lambda_function {
        lambda_function_arn = var.lambda_notification.arn
        events              = var.lambda_notification.events
        filter_prefix       = try(var.lambda_notification.filter_prefix, null)
        filter_suffix       = try(var.lambda_notification.filter_suffix, null)
      }
      ```

    The completed `modules/s3_notification/main.tf` file contains the following configuration:

    ```hcl
    resource "aws_lambda_permission" "allow_bucket" {
      statement_id  = "AllowExecutionFromS3Bucket"
      action        = "lambda:InvokeFunction"
      function_name = var.lambda_notification.arn
      principal     = "s3.amazonaws.com"
      source_arn    = var.bucket.arn
    }

    resource "aws_s3_bucket_notification" "bucket_notification" {
      bucket = var.bucket.id

      lambda_function {
        lambda_function_arn = var.lambda_notification.arn
        events              = var.lambda_notification.events
        filter_prefix       = try(var.lambda_notification.filter_prefix, null)
        filter_suffix       = try(var.lambda_notification.filter_suffix, null)
      }

      depends_on = [aws_lambda_permission.allow_bucket]
    }
    ```

9. In the **TERMINAL**, run the following command to zip the contents of the module folder into an archive:

    ```bash
    cd modules/s3_notification && zip -r s3_notification.zip . && cd ../../
    ```

10. Run the following command to copy your module to the S3 bucket:

    ```bash
    aws s3 cp modules/s3_notification/s3_notification.zip s3://$BUCKET_NAME/modules/
    ```

11. Run the following command to print the name of your bucket. You will use the full name in the next step:

    ```bash
    echo "$BUCKET_NAME"
    ```

12. In the `main.tf` file of your primary Terraform configuration, replace the `aws_lambda_permission` and `aws_s3_bucket_notification` resources with the following moved blocks and module configuration:

    ```hcl
    moved {
      from = aws_lambda_permission.allow_bucket
      to   = module.s3_notification.aws_lambda_permission.allow_bucket
    }

    moved {
      from = aws_s3_bucket_notification.bucket_notification
      to   = module.s3_notification.aws_s3_bucket_notification.bucket_notification
    }

    module "s3_notification" {
      source = "s3::https://ps-tf-bucket-<random-id>.s3.us-east-1.amazonaws.com/modules/s3_notification.zip"
      bucket = {
        arn = module.s3_bucket.s3_bucket_arn
        id  = module.s3_bucket.s3_bucket_id
      }
      lambda_notification = {
        arn    = aws_lambda_function.s3_handler.arn
        events = ["s3:ObjectCreated:*"]
      }
    }
    ```

    Replace `ps-tf-bucket-<random-id>` with the full bucket name you echoed earlier.

    > **Note:** The module `source` value must contain the exact bucket name. Terraform module sources cannot use variables, so you must enter the bucket name directly.

13. Run the following command to initialize the new module:

    ```bash
    terraform init
    ```

    When initialization finishes, Terraform displays:

    ```text
    Terraform has been successfully initialized!
    ```

14. Run the following command to see Terraform's plan for the new module:

    ```bash
    terraform plan
    ```

    Verify that Terraform reports both resources as moved and displays:

    ```text
    Plan: 0 to add, 0 to change, 0 to destroy.
    ```

    > **Note:** The `moved` blocks map the existing resource addresses to their new addresses inside the module. This allows Terraform to update the state without destroying and recreating the resources.

15. Run the following command to execute the move:

    ```bash
    terraform apply --auto-approve
    ```

    Terraform will complete the move of the resources and output:

    ```text
    Apply complete! Resources: 0 added, 0 changed, 0 destroyed.
    ```

### Use module versioning

You will modify the module to use lists of notification configurations, creating a new module version.

1. In the `variables.tf` file, change the `lambda_notification` variable to:

    ```hcl
    variable "lambda_notification" {
      description = "Lambda Function notification configuration object"
      type = list(object({
        arn           = string
        events        = list(string)
        filter_prefix = optional(string)
        filter_suffix = optional(string)
      }))
    }
    ```

2. Add a new variable, `sqs_notification`:

    ```hcl
    variable "sqs_notification" {
      description = "SQS notification configuration object"
      type = list(object({
        arn           = string
        events        = list(string)
        filter_prefix = optional(string)
        filter_suffix = optional(string)
      }))
      default = []
    }
    ```

3. In `modules/s3_notification/main.tf`, replace the `aws_lambda_permission` resource with the following configuration:

    ```hcl
    resource "aws_lambda_permission" "allow_bucket" {
      for_each = { for idx, n in var.lambda_notification : idx => n }

      statement_id  = "AllowExecutionFromS3Bucket-${each.key}"
      action        = "lambda:InvokeFunction"
      function_name = each.value.arn
      principal     = "s3.amazonaws.com"
      source_arn    = var.bucket.arn
    }
    ```

4. Replace the `aws_s3_bucket_notification` resource with the following configuration:

    ```hcl
    resource "aws_s3_bucket_notification" "bucket_notification" {
      bucket = var.bucket.id

      dynamic "lambda_function" {
        for_each = var.lambda_notification

        content {
          lambda_function_arn = lambda_function.value.arn
          events              = lambda_function.value.events
          filter_prefix       = try(lambda_function.value.filter_prefix, null)
          filter_suffix       = try(lambda_function.value.filter_suffix, null)
        }
      }

      dynamic "queue" {
        for_each = var.sqs_notification

        content {
          queue_arn     = queue.value.arn
          events        = queue.value.events
          filter_prefix = try(queue.value.filter_prefix, null)
          filter_suffix = try(queue.value.filter_suffix, null)
        }
      }
      depends_on = [aws_lambda_permission.allow_bucket]
    }
    ```

5. In the **TERMINAL**, run:

    ```bash
    cd modules/s3_notification && rm s3_notification.zip
    ```

    Then run:

    ```bash
    zip -r s3_notification.zip . && cd ../../
    ```

    These commands will create a new version of the module package.

6. Run the following command to upload the package to S3:

    ```bash
    aws s3 cp modules/s3_notification/s3_notification.zip s3://$BUCKET_NAME/modules/
    ```

7. Return to the AWS Console S3 **ps-tf-bucket-** browser tab, click the **Refresh Objects** button, then click `modules/`.
8. Click `s3_notification.zip`, and then select the **Versions** tab.

    You should see two versions of the module. The first is the version you created earlier, and the latest version supports a `list` and SQS notifications.

9. Click the link for the older version. It's the only version with a link.
10. Copy the query string that begins with `?versionId=` from the **Object URL**.
11. Return to VS Code.
12. In the `main.tf` file of your infrastructure, modify the `source` property of the `s3_notification` module:

    ```hcl
    source = "s3::https://ps-tf-bucket-<random-id>.s3.us-east-1.amazonaws.com/modules/s3_notification.zip?versionId=<version-id>"
    ```

    Replace `<random-id>` and `<version-id>` with the values from your environment.

13. In the **TERMINAL**, run the following command to reinitialize Terraform:

    ```bash
    terraform init
    ```

    Verify that the output shows Terraform downloading the specified module version.

    > **Note:** Pinning the module to a specific object version prevents Terraform from using later module changes until you update the version ID.
