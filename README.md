# Spot Tag Bot for Digital Assets

[中文版本](./README_ZH.md)

The Spot Tagging Bot for Digital Assets solution leverage the machine learning models to help customers quickly deploy an automated Digital Asset Inspection System in the AWS (Ningxia) region operated by NWCD and the AWS (Beijing) region operated by Sinnet. Spot Bot support label digital assets( e.g., unstructured data such as photos, PDF documents, videos, etc.) stored inside Amazon S3 at low cost (e.g., unstructured data such as photos, PDF documents, videos, etc.), these knowledge labels will help customers automate business processes and create precise knowledge maps. Robot warehouses built on top of open source datasets can support multiple types of tasks, such as OCR identification of text pictures, text classification of documents, image classification of vehicle models, etc.  Customer can use bots directly and build customised bot by fine-tune your own model.

- **Applicable regions:** cn-northwest-1 (Ningxia), cn-north-1 (Beijing)
- **Version:** v1.0
- **Estimated deployment time:** 20min

If you have problems during your deployment, you can contact us at [GitHub Issues](https://github.com/aws-samples/spot-tag-bot-for-digital-assets/issues).

## Architecture

You can choose to deploy the digital asset disk robot solution directly. Here are the schema of the scheme.

![Architect](assets/architect.png)

## Step 1: Start the CloudFormation stack

This automated AWS CloudFormation template deploys Spot Tag Bot for Digital Assets solution on AWS Cloud.

You are responsible for the cost of the AWS services you use when running this solution. For more details, see the Expenses section. For full details, see the pricing page for each AWS service that will be used in this solution.

1. Log in to the AWS Management Console and click the button below to start the AWS CloudFormation template.

 [![Launch Stack](assets/launch-stack.png)](https://cn-northwest-1.console.amazonaws.cn/cloudformation/home?region=cn-northwest-1#/stacks/create/template?stackName=spot-bot&templateURL=https:%2F%2Faws-solutions-reference.s3.cn-north-1.amazonaws.com.cn%2Fspot-bot%2Fv1.0.0%2Fspot-bot-china.template)
 
2. By default, the template is launched in the AWS Ningxia region. To launch the solution in another AWS region, use the zone selector in the console navigation bar.

3. On the **Create Stack** page, confirm that the correct template URL is displayed in the **Amazon S3 URL** text box and select **Next**.

4. On the **Specify Stack Details** page, assign a name to the solution stack.

5. Under **Parament**, look at the parameters of the template and modify as needed. This solution uses the following defaults.

2. Choose **Next Step**.

3. On the **Configure Stack Options** page, select Next.

4. On the **Audit** page, review and confirm the settings. Ensure that the confirmation template will create the AWS Identity and Access Management (IAM) resource box is selected.

5. Select **Create Stack** to deploy the stack.

You can view the status of the stack in the **Status** column of the AWS CloudFormation Console. You should see the status CREATE_Complete in about 20 minutes.

## FAQ

**Q: How does the asset disk robot solution work?**

The Spot Tag Bot for Digital Assets solution includes an AWS CloudFormation template to help you deploy quickly in your AWS account.This template initiates all the resources and permissions settings you need to deploy this solution.
When the template is deployed, you can specify the S3 path of the data assets you need to live and the robot you need to start. Spot Tag Bot for Digital Assets solution supports many data asset types, including text, video, pictures, etc.Upon launch, the specified robot generates a list of tasks based on the content of the current S3, which contains digital assets to be processed, such as 1,000 videos that need to be labeled.Specific tasks are segmented (Batch), and then multiple instances of robots handle their respective task segments, if there are a total of 10 robots, each clip may include 100 videos.These robot instances are all running on Spot Instance, so they are computationally good value for money.After processing the current task, the robot writes the results to Elastic Search and S3.If an exception occurs to a robot instance, the task is given to another robot instance to redo it.Customers can query the results of a task through Elastic Search and understand the execution status of the entire task.

Each robot consists of two layers, one layer of implementation of business requirements, such as OCR robots can complete OCR tasks, but specific OCR tasks may require multiple models to collaborate, such as one model that frames the text section out, and the other model is only responsible for identifying the box's good text, which is the second model. layer to provide capability support to the business tier.

**Q: Can I use my own data for secondary training?**

Yes, there is a container-based training framework in the Spot Tag Bot for Digital Assets solution.Users can use AWS Sagemaker or other Notebook hosting services to open training framework software and import their own labeled data for training.After training results users can export into the robotic framework of asset disk live robotics solutions. Spot Tag Bot for Digital Assets solution will use a model after secondary training for reasoning
