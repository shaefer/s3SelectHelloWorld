# S3Select Hello World Example

https://www.serverless.com/blog/cicd-for-serverless-part-1/
https://www.serverless.com/blog/cicd-for-serverless-part-2/

Getting started with Lambda isn't hard at all. But if you are shooting for a super simple API you are still left with a lot of boilerplate things and missing pieces to make it really useful. Each which have their own small gotchas. Testing, deployments, API Gateway, cors, staged deployments, database setup, roles, permissions, javascript modules, dependency install, etc. It can still be a decent amount of work to get to something straightforward: A datasource accessible through lambda driven by a restful API written with Javascript with no hoops for pulling in additional js dependencies. Serverless helps you get there without worrying about all that boilerplate.

## Do this first (prerequisites): 
- [Follow Serverless setup guide](https://www.serverless.com/framework/docs/providers/aws/guide/installation/) for 3 things:
    1. Install Node
    1. Install Serverless
    1. Setup AWS - mostly setting up credentials

If you are looking for a first-time guide to serverless and lambda's please check out [this serverless example project](https://github.com/shaefer/serverless_example) first.

## Getting Started
1. Fork the project. 
1. `npm install`
1. Look through the project:
    - **Understand the document we are querying against and the query we are using**
        - Look at `serverless.yml` for the definitions of things going into AWS. 
        - Make sure to check `service`, `region`, and `stage` on the provider entry in `serverless.yml` to your desired otherwise you'll deploy to `us-west-2` and the stage will be named `dev` The first time you create all this in AWS you probably should go look through everything that got created. It is all happening with CloudFormation and it is doing a lot of nice things for you and all the names and such are coming from the serverless.yml file and are under your control.
1. Run it locally `serverless invoke local --function s3SelectQuery` This is like hitting your lambda live with the earlier mentioned URI. 
1. Run `serverless deploy` to create the lambda and dynamodb table in AWS. The output for the deploy will show success and give you the url for the deployed API gateway endpoint that you can hit to test it live.
1. *OPTIONAL BUT IMPORTANT*: If you forgot something and want to rollback...**BEFORE** you change anything in the serverless.yml just run a `serverless remove` and it will delete all the resources it just created...or try to. Since serverless created everything with Cloudformation it can remove it too. Find more details in the [serverless docs](https://www.serverless.com/framework/docs/providers/aws/cli-reference/remove/).

https://docs.aws.amazon.com/AmazonS3/latest/API/API_SelectObjectContent.html
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html
