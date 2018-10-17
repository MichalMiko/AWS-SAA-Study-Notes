# Architecting for the Cloud - AWS Best Practices 

The whitepaper is available for download at https://d0.awsstatic.com/whitepapers/AWS_Cloud_Best_Practices.pdf or in the `whitepapers` folder.



## Business Benefits of Cloud

- Almost zero upfront infrastructure investment
- Just-in-time Infrastructure - auto scaling etc.
- More efficient resource utilization
- Usage-based costing (Utility Billing) - Pas By the hour, No contracts needed
- Reduced "time to market" - easily copy infrastructure to another country (region)

## Technical Benefits of Cloud

- Automation - "Scriptable Infrastructure" / Infrastructure as Code
- Auto-scaling
- Proactive Scaling
- More Efficient Development lifecycle - Continuous Integration/ Continuous Delivery
- Improved Testability - test immediately
- Disaster Recovery and Business Continuity - Failover to additional infrastructure in the cloud

## Design for Failure

Rule of thumb: Be a pessimist when designing architectures in the cloud; assume things will fail. In other words, always design, implement and deploy for automated recovery form failure.

In particular, assume that hardware will fail. Assume That outages will occur. Assume that some disaster will strike your application. Assume that you will be slammed with more than the expected number of requests per second some day. Assume that with time your application software will fail too.

By being a pessimist, you end up thinking about recovery strategies during design time, which helps in designing an overall system better.

Netflix has a Disaster Monkey and a  Chaos Snail

## Decouple Your Components

If you have to decouple something search for SQS in answers.

Build Components that do not have tight dependencies on each other. 

If one component is going to:

- die (fail)
- sleep (not respond)
- remain busy (slow to respond)

the other components should continue to work as if no failure is happening.

Each component of your application should interact asynchronously with others and treat each other as a "black box"

Example:

App Server  < SQS > Web Server < SQS > Database 

## Implement Elasticity

Elasticity can be implemented in three ways:

1. **Proactive Cyclic Scaling**: Periodic scaling that occurs at fixed interval (daily, weekly, monthly, quarterly) - app busy at the end of the month
2. **Proactive Event-based Scaling**: Scaling just when you are expecting a big surge of traffic request due to a scheduled business event (new product launch, marketing campaigns)
3. **Auto-scaling base on demand**: By using a monitoring service, your system can send triggers to take appropriate actions so that it scales up or down based on metrics (utilization of the servers or network I/O, for instance)

## Secure You Application

Section 11 Lecture 100

![Image result for aws security groups best practices](C:\git\AWS-SAA-Study-Notes\docs\images\aws-security-best-practises.png)  