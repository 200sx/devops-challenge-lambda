# Lambda DevOps Challenge

Preface: Thanks in advance for providing me an opportunity to learn more about SAM and Lambda deployment tooling. Its something I've been meaning to get around to doing but never had it prioritised until now. I'm also a backend guy so it was fun to jump into some JavaScript.


Anything below this line pertains to the technical evaluation (deployment documentation etc.)

API URL: https://jyc18149u8.execute-api.ap-southeast-2.amazonaws.com/Prod/hello (handler.js listens on /hello)  
AWS Console: https://201293276503.signin.aws.amazon.com/console
AWS Region: ap-southeast-2

Reach out to me personally for details.

***

## Initial Setup
Welcome to this project. It deploys a Lambda based application via SAM. Everything is IaC. 

### Setting up local environment
To work with this application, refer to your OS/distro's documentation to install the following;
- npm 
- aws-cli
- sam
- docker (required for local API development)

To run unit tests
``` sh
npm run test # runs the stub unit-tests as per package.json configs, provides code coverage report 
```

### Deployment process
In the future - a CI/CD environment should be set up to automate this process. Not only does it free up engineering time but it also enforces TDD as the testing suite must be robust enough so that one is confident automated deployments will break live environments due to poor test code coverage and integration tests.

**Local Testing**
``` sh
sam local start-api # this starts up a local API server, on port 3000 as per SAM templates
```

**To deploy to AWS**
``` sh
sam deploy # deploys code to production, will also run "sam package" so no need to run manually
```

******

## What I have done
- Exposed the API via AWS SAM
    - GitOps compliant (IaC, configuration files, stateless code)
- Created an Ops user account with access to required resources explicitly for perfomance/operational information (as per spec)
    - ReadOnlyAccess to AWS Lambda, CloudFormation, CloudWatch
    - I've given the user full read access to the aforementioned AWS resources, if time was not a limit, this could be limited to specific required ARNs, and the users' policies could also be a CFN stack for IaC purposes
- Provided a stub testing suite for local JS devs (even though function can't really be tested as its non-deterministic)
    - Code coverage reports part of test suite


## Further Improvements
- Use AWS Config to run application against required standards (e.g. AWS WAF)
- Set up AWS CloudWatch Alarms for basic alerting. On the topic of Monitoring and Alerting, if we had a properly serious deployment, one could
    - Send data to AWS ELK to collect APM, run queries on what events cause failures, set up robust alerting
    - CI/CD events/logs could also be pushed into the monitoring software if required to measure DevOps related KPIs
- Improve actual codebase (ES6 compliance, use modern features, promises etc)
- Integrate with SAST tooling e.g. SonarCloud (managed service) or CloudConformity (hehe)
