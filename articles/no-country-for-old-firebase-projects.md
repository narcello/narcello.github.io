---
title: No Country for Old Firebase Projects — My Unexpected Journey into AWS
---

# No Country for Old Firebase Projects — My Unexpected Journey into AWS

Recently I created an simple and static page for a local lawer here called Beatriz Maia, aka my wife. Hosted in cloudflare, all good, working fine. Until I decided to move it to the AWS and start this Odissey. How and why this whole time, in 10 years, I procastinate so long to dive into this thing. idk.

Always using Firebase for freelance, MPVs, personal projects and even for a production chat feature from a company that I worked for in 2019. IMHO Pros and Cons of Firebase: too easy to use, this fits for PRO and CON. Never felt that I was dealing with the infrastructure, db, network, security, never felt that I was dealing with something that companies used to deal.

---

- **Goal:** Learn AWS
- **How:** Moving a static site there and then add some features.
- **Why:** I want/need.

---

I'll start writing down just using my memory.

I used ChatGPT to guide me through the process, where do I needed to go, what to do, why to do this and that, but never "create this to me, here is my credentials", nothing with terraform, aws cli, cdk, all manually like at the stone age. I started and then, tons of concepts, which some of them I already knew but others was new to me: Cloudfront, Route53, ACL, S3, WAF, IAM, Invalidation.

After I created everything, and all is running, 1 week later Im here writing a blog because I don't remember things that I did. Of course I know, but the details and the clear architecture is not in my head. probably I spend 1/2 days doing this, later I added a testimonials sections to visitors add some comments about last or current experiences about Beatriz work. More concepts: API Gateway, DynamoDB, Lambda, more IAM Roles, Policies.

Then visitors add comments but I cannot let all comments show in the page for obvious reasons. I needed a moderation, which means admin page, which means restrict area, which means more concepts: Cognito, User Pools, more IAM roles and permissions.

Last but not least, I decided to add the IA to pre-triage the visitor, maybe your case don't fit inside the Beatriz office area, maybe does. Yes, more concepts: Bedrock, Budget alerts, Guardrails.

This is my description just writing down what I remember, now I'll ask for all services and terminologies used last week for AI:

- Route 53
- ACM
- CloudFront
- S3
- WAF
- API Gateway
- Lambda
- DynamoDB
- Cognito
- Bedrock
- AWS Budgets
- IAM
- CloudWatch

Ok, good memory, lets dive into each one and then connect everything.

---

## Route 53

## ACM

Generate a SSL certification which will be used in the cloudfront

## CloudFront

Will serve files that you have in S3, like your index.html

## S3

Storage, where you put your build folder, images, index, html, your page is there

## WAF

Web Application Firewal, some protection layer which is in front of the cloudfront. Do some XSS and bunch of other protections in your app

## API Gateway

This will call your correct lambda. When you deploy an Express server, we have the server running with the endpoints which we going to call like GET /posts. This goes to the server, to this route and do whatever needs to do. Working with lambda, serverless functions, we need the API Gateway in front to expose this route. Lamba has the logic, what will be executed, but you don't call the lambda directly, you call the API Gateway, and the request is forward to lambda.

## Lambda

Serverless functions which doesn't export the api routes, at least in what I tested and used until now. You add here the business logic, what will be executed. API Gateway will handle the requests and call the correct lambda based on the request.

## DynamoDB

NoSQL Key-Value database

## Cognito

Auth provider service. Here you can configure the authentication in your app, the sign in page, customize it, add some custom domain, manage the users, create a user pool, add application that will use the auth flow. User pool I think it's something created to isolate users, if you think about multi-tenant application, each app must have a user pool.

## Bedrock

IA service. You can create the instance, select the model, create the constraints, fine tune it, rules. You can create create a different guardrails and attach to the bedrock instance that you created. You will have a endpoint which will be called by lambda to process the data.

## AWS Budgets

Important to create alerts of you usage and you not surprise at the end of the month. You can create a global budget for your whole account of based on one specific project or service.

## IAM

So important in all services. Allows aws services comunicate between them. When you have a lambda doing some change in dynamoDB and later updatind some file in S3. This lambda will need a role to do this. This role must contains the polices. Which is basically something like:

- the service which use the role with this police, will be able to read, post and patch the DynamoDB
- the service which use the role with this police, will be able to update a file in S3

Of course, in tech language, I just translate it.

## CloudWatch

Usefull to
