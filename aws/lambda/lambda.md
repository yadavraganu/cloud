# What is lambda
- You can use AWS Lambda to run code without provisioning or managing servers.
- Lambda runs your code on a high-availability compute infrastructure and performs all of the administration of the compute resources,
  including server and operating system maintenance, capacity provisioning and automatic scaling, and logging.
- With Lambda, all you need to do is supply your code in one of the language runtimes that Lambda supports.
- You organize your code into Lambda functions. The Lambda service runs your function only when needed and scales automatically.
- You only pay for the compute time that you consume,there is no charge when your code is not running
# Lambda Concepts
## Concurrency
Concurrency is the number of in-flight requests that your AWS Lambda function is handling at the same time. For each concurrent request,  
Lambda provisions a separate instance of your execution environment. As your functions receive more requests, Lambda automatically handles  
scaling the number of execution environments until you reach your account's concurrency limit. By default, Lambda provides your account with  
a total concurrency limit of 1,000 concurrent executions across all functions in an AWS Region.

Lambda invokes your function in a secure and isolated execution environment. To handle a request, Lambda must first initialize an execution  
environment (the Init phase), before using it to invoke your function (the Invoke phase):  
![image](https://github.com/yadavraganu/cloud/assets/77580939/9eded5b7-41a8-4e62-a6f6-db81737b0ca7)  
When Lambda finishes processing the first request, this execution environment can then process additional requests for the same function.  
For subsequent requests, Lambda doesn't need to re-initialize the environment  
![image](https://github.com/yadavraganu/cloud/assets/77580939/41e42c5a-d6fd-49ef-b931-bdd1bf86d265)

In practice, Lambda may need to provision multiple execution environment instances in parallel to handle all incoming requests.  
When your function receives a new request, one of two things can happen:
- If a pre-initialized execution environment instance is available, Lambda uses it to process the request.
- Otherwise, Lambda creates a new execution environment instance to process the request.
![image](https://github.com/yadavraganu/cloud/assets/77580939/7aa3446d-469c-4c62-81cc-6c83c2129367)

__Reserved concurrency__ – This represents the maximum number of concurrent instances allocated to your function. When a function has reserved concurrency, no other function can use that concurrency. Reserved concurrency is useful for ensuring that your most critical functions always have enough concurrency to handle incoming requests. Configuring reserved concurrency for a function incurs no additional charges.

__Provisioned concurrency__ – This is the number of pre-initialized execution environments allocated to your function. These execution environments are ready to respond immediately to incoming function requests. Provisioned concurrency is useful for reducing cold start latencies for functions. Configuring provisioned concurrency incurs additional charges to your AWS account.
## Environment Variables
You can use environment variables to adjust your function's behavior without updating code. An environment variable is a pair of strings that is    
stored in a function's version-specific configuration. The Lambda runtime makes environment variables available to your code and sets additional  
environment variables that contain information about the function and invocation request (reserved or in built variables).  
Environment variables are not evaluated before the function invocation. Any value you define is considered a literal string and not expanded.

![image](https://github.com/yadavraganu/cloud/assets/77580939/bc9d89f3-4837-4758-8e90-1c7cceb80730)
