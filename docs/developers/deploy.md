## DevOps - Production Deployment

We use various cloud services for the platform, for example AWS S3 for storing data and metadata, and the application runs on Docker Cloud.

We have fully automated the deployment of the platform including the setup of all necessary services so that it is one command to deploy. Code and instructions here:

https://github.com/datahq/deploy

Below we provide a conceptual outline.

### Outline - Conceptually

<div class="mermaid">
graph TD

  user[fa:fa-user User] --> frontend[Frontend]
  frontend --> apiproxy[API Proxy]
  frontend --> bits[BitStore - S3]
</div>

### New Structure[docker]

This diagram shows the current deployment architecture.

<div class="mermaid">
graph TD

  user[fa:fa-user User]
  bits[BitStore]
  cloudflare[Cloudflare]

  user --> cloudflare
  cloudflare --> docker
  cloudflare --> bits
  docker[Docker - Node JS Application] --> apiproxy[API Proxy]
  docker --> bits
</div>

### Old Structure[heroku]

This diagram shows the current deployment architecture.

<div class="mermaid">
graph TD

  user[fa:fa-user User]
  bits[BitStore]
  cloudflare[Cloudflare]

  user --> cloudflare
  cloudflare --> heroku
  cloudflare --> bits
  heroku[Heroku - Flask] --> rds[RDS Database]
  heroku --> bits
</div>

### Old Structure[AWS Lambda - Flask via Zappa]

We are no longer using AWS in this way. However, we have kept this for historical purposes and in case we return to AWS

<div class="mermaid">
graph TD

  user[fa:fa-user User] --> cloudfront[Cloudfront]
  cloudfront --> apigateway[API Gateway]
  apigateway --> lambda[AWS Lambda - Flask via Zappa]
  cloudfront --> s3assets[S3 Assets]
  lambda --> rds[RDS Database]
  lambda --> bits[BitStore]
  cloudfront --> bits
</div>