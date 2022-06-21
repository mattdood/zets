---
path: '/2022/6/aws-elastic-beanstalk-customization-20220621132728'
title: 'aws elastic beanstalk customization'
date: '20220621132728'
category: 'aws'
tags: ['developer associate', 'certification', 'elastic beanstalk']
---

# aws elastic beanstalk customization
Customization of the Elastic Beanstalk environment is done in a few different ways
depending on the Amazon Linux version (1 or 2).

## For pre-Amazon Linux 2 environments
* configuration file - define packages to install, create linux users and groups,
run shell commands, enable services, and configure load balancers
* YAML or JSON - these files are written in YAML or JSON format
* Constraints - the file must have a `.config` extension and be inside a folder
called `.ebextensions` in the top-level directory of your application source code
bundle

Example - `myhealthcheckurl.config`:
```
{
    "option_settings": [
        {
            "namespace": "aws:elasticbeanstalk:application",
            "option_name": "My application healthcheck URL",
            "value": "/healthcheck"
        }
    ]
}
```

The above configures an application health check URL that will be used by a load
balancer, which will make an HTTP request to the specified path to check if the
instances are healthy.

## Amazon Linux 2 environments
Use the `Buildfile`, `Procfile` and `platform hooks` whenever you need to do additional
configuration during the application building period.

### Buildfile
* Great for commands that run for short periods and then exit upon task completion.
    * Good examples are shell scripts
* Root directory - create your `Buildfile` in the root directory of your application source
* Format - `<process_name>:<command>`
    * Example: `make: ./build.sh` <- reference a script in your source code bundle

### Procfile
* Used for long-running processes (like commands to start and run the application)
* Root directory - create a file called Procfile in the root directory of your application source
* Elastic Beanstalk expects processes defined in the `Procfile` to run continuously
    * Any processes that terminate will be monitored and restarted
* Format - Same as the `Buildfile`, using key:value pairs
    * `<process_name>: <command>`

Example:
```
web: bin/myserver
app: bin/myapp
```

### Platform hooks
* This is for custom scripts or executable files that you would like to be run at
a **chosen stage** of the EC2 provisioning process.
* Stored in dedicated directories in your application source code
* The build directories are:
    * `.platform/hooks/prebuild` - files that you want to run before it builds, sets up,
    and configures the application and web server
    * `.platform/hooks/predeploy` - files that you want to run after it sets up and
    configures the application and web server but before it deploys them to the final
    runtime location
    * `.platform/hooks/postdeploy` - files that run after Elastic Beanstalk has deployed
    the application
* Each stage is optional, only include the directories that are required

## Exam tips
* Amazon Linux 1 can modify the Elastic Beanstalk environment using the `.ebextensions` folder
    * Files need a `.config` extension
* Amazon Linux 2:
    * `Buildfile` - for scripts that exist upon completion
    * `Procfile` - used in long running processes (like starting the app)
    * `Platform hooks` - several stages offering the ability to customize at each stage

