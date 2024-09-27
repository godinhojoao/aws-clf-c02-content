# AWS Architecting

## Well Architected Framework General Guiding Principles

- **Stop guessing capacity**: Automate scalability to meet demand.
- **Test at production scale**: Simulate real-world usage.
- **Automate for experimentation**: Make experimentation easier.
- **Evolve architectures**: Adapt to changing requirements.
- **Data-driven**: Use data to guide decisions.
- **Improve with game days**: Practice failure scenarios.

## AWS Well Architected Framework – 6 Pillars

1. **Operational Excellence**: Run, monitor, and improve systems.
2. **Security**: Protect information and systems.
3. **Reliability**: Ensure system recovery and meet demand.
4. **Performance Efficiency**: Use resources efficiently.
5. **Cost Optimization**: Minimize costs while delivering value.
6. **Sustainability**: Minimize environmental impact.

## Operational Excellence Design Principles

- **Operations as code**: Use Infrastructure as Code (IaC).
- **Frequent, reversible changes**: Ensure easy rollback.
- **Anticipate failure**: Learn from failures.
- **Use managed services**: Reduce operational burden.
- **Observability**: Monitor performance, reliability, and cost.

## AWS Cloud Best Practices – Design Principles

- **Scalability**: Vertical and horizontal scaling.
- **Disposable resources**: Servers should be disposable and easily replaceable.
- **Automation**: Use Serverless, IaaS, Auto Scaling.
- **Loose coupling**: Avoid monolithic designs; smaller, independent components.
- **Services over servers**: Use managed services, not just EC2.

## Security Design Principles

- **Strong identity foundation**: Centralize and reduce credentials.
- **Traceability**: Integrate logs and metrics.
- **Security at all layers**: Implement security throughout the architecture.
- **Data protection**: Use encryption and access control.
- **Automate security**: Automate detection and response.
- **Incident preparation**: Simulate security events for prevention.

## Reliability Design Principles

- **Test recovery**: Automate failure simulations.
- **Auto recovery**: Automatically recover from failures.
- **Horizontal scaling**: Distribute load to avoid single points of failure.
- **Capacity management**: Use Auto Scaling to optimize resources.

## Performance Efficiency Design Principles

- **Advanced tech as services**: Focus on product development.
- **Global deployments**: Deploy in multiple regions quickly.
- **Serverless**: Reduce server management.
- **Experiment often**: Test different configurations.

## Cost Optimization Design Principles

- **Pay-per-use**: Only pay for what you use.
- **Efficiency measurement**: Track resource usage.
- **Avoid data centers**: Use AWS-managed infrastructure.
- **Tagging for cost analysis**: Attribute and track expenses accurately.

## Sustainability Design Principles

- **Track environmental impact**: Establish sustainability KPIs.
- **Maximize utilization**: Right-size workloads.
- **Adopt efficient hardware**: Use new, energy-efficient technologies.
- **Leverage managed services**: Reduce infrastructure and automate best practices.

## AWS Well-Architected Tool

- **Free tool** to review your architecture against best practices in the 6 pillars.
- **Get insights**: Videos, documentation, reports, and dashboards.

## AWS Customer Carbon Footprint Tool

- **Track and reduce** your AWS carbon emissions to meet sustainability goals.

## AWS Cloud Adoption Framework (AWS CAF)

- Supports cloud transformation using 6 perspectives: Business, People, Governance, Platform, Security, and Operations.
- **Business Perspective**: Align cloud investments with business goals.
- **People Perspective**: Facilitate organizational growth and learning.
- **Governance Perspective**: Manage risks and maximize cloud benefits.
- **Platform Perspective**: Build a scalable cloud platform.
- **Security Perspective**: Ensure data confidentiality and integrity.
- **Operations Perspective**: Deliver services that meet business needs.

## AWS Cloud Transformation

- **Domains**: Technology, Process, Organization, Product.
- **Phases**: Envision, Align, Launch, Scale.

## AWS Right-Sizing - (start small, the cloud is elastic so you can scale up when needed)

- Match EC2 instances to workload needs for cost optimization.
- Use **CloudWatch**, **Cost Explorer**, and **Trusted Advisor** for ongoing adjustments.

## !Important
- **Operational Excellence**: Having infrastucture as Code (IaC), CI/CD pipelines...