# Sample PHP Serverless HTTP application with Bref

In this sample using AWS Lambda

## Prequiesition
- PHP 7.2+
- AWS account (Must have minimum permission: CloudFormation, CloudWatch, Lambda, S3, API Gateway, and etc.)
- Node

## Install
1. Get AWS Credential
2. Install serverless
```
npm install -g serverless
```
3. Config serverless with AWS
```
serverless config credentials --provider aws --key <key> --secret <secret>
```
4. Install bref
```
composer require bref/bref
```

## Create app

```
vendor/bin/bref init
```

will show

```
What kind of lambda do you want to create? (you will be able to add more functions later by editing `serverless.yml`) [PHP function]:
  [0] PHP function
  [1] HTTP application
  [2] Console application
```

and type 1

## Config app in serverless.yml

***function*** : your function name (in my sample is "reactphp-bref-function")

***region*** : set to your AWS region such as ap-southeast-1

***layers*** : runtime of your app

PHP functions: php-74 and php-73
The simplest way to write a lambda is to write one in the form of a PHP function.

This runtime works great for non-HTTP applications.

HTTP applications: php-74-fpm and php-73-fpm
This runtime uses PHP-FPM to run HTTP applications on AWS Lambda.

This runtime is the easiest to start with: it works like traditional PHP hosting and is compatible with Symfony and Laravel.

(Read more at https://bref.sh/docs/runtimes/#bref-runtimes)

## Deployment (Dev)

```
serverless deploy
```

## Invocation
Check link to access after deploy (link is generated from API Gateway)

## Invocation (On my localhost)

```
php -S localhost:8000 index.php
```

## Deployment (Production)
If everything working, you can duplicated folder or convert dev function to production by remove dev dependencies, dev config

```
composer install --prefer-dist --optimize-autoloader --no-dev
```

and then deploy again

```
serverless deploy
```

## Delete
If you want to delete function

```
serverless remove
```