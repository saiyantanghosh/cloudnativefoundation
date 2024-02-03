![](cn.PNG)
# What is Cloud?
Cloud is an IT infrastructure that supports the delivery of computing resources to consumers according to the cloud computing model.

The National Institute of Standards and Technology (NIST) defines cloud computing as follows
*Cloud computing is a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction.*

Elasticity is the main characteristic of the cloud. on-demand scale in and out.
*Elasticity is the degree to which a system is able to adapt to workload changes by provisioning and de-provisioning resources in an autonomic manner, such that at each point in time the available resources match the current demand as closely as possible*
# When will consider cloud?
Goals - if below one of them is objective to your business, then consider cloud
**Speed** - faster and more flexible delivery
**Resilience** - availability, and stability
**Scale** - elasticity and dynamic scaling
**Cost** - efficiency and cost-optimization
# Cloud Deployment Models 
There is no restriction on where cloud infra should be or who will manage it.
Below 3 cloud deployment models for delivering cloud services -
* private cloud - infra provisioned to be used by one organization because of security compliance, law ( GDPR) - mostly banking & healthcare.
* public cloud - infra managed by the cloud provider. AWS, azure
* hybrid cloud - public + private
* multi cloud - multiple public cloud OR multiple managed services (saas)
# Cloud Service models 
What each deployment model is providing.

[](https://cloud.google.com/learn/paas-vs-iaas-vs-saas)

# What is cloud-native?

*Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, microservices, immutable infrastructure, and declarative APIs exemplify this approach.*

*These techniques enable loosely coupled systems that are resilient, manageable, and observable. Combined with robust automation, they allow engineers to make high-impact changes frequently and predictably with minimal toil.*

## Three Ps of Cloud Native - 
* Platform -  CN apps run on a dynamic distributed environment - cloud ( private, public, hybrid) 
* Properties - CN apps are designed for scalable, loosely coupled, resilient, manageable, and observable.
* Practice - practices around cn apps - DevOps, continuous delivery, and automation

# Cloud native app properties 
 ## Scalability
 HS and VS scalability is a prerequisite of elasticity.
 ## Loosely coupling
 decomposes the system into modules ( modularizations) - loose coupling, highly cohesive
  Parnas identified three benefits of modularization:6
  
  **Managerial**—Since each module is loosely coupled, the team responsible for it should not need to spend much time coordinating and communicating with other teams.
  
  **Product flexibility**—The overall system should be flexible since each module is evolved independently of the others.
  
  **Comprehensibility**—People should be able to understand and work with a module without having to study the whole system.
  
   **Watch out for distributed monolith/modular monolith - tightly coupled, non-cohesive microservice because of lack of proper modularization.**
 ## Resilience
   *Resilience is “the capability of a hardware-software network to provide and maintain an acceptable level of service in the face of faults and challenges to normal operation*
    **Fault**—A fault is a defect that produces an incorrect internal state either in the software or the infrastructure. For example, a method call returns a null value, even if its specification mandates that a non-null value is returned.
    
    **Error**—An error is a discrepancy between the expected behavior of a system and the actual one. For example, due to the preceding fault, a NullPointerException is thrown.
    
    **Failure**—When a fault is triggered and results in an error, a failure might occur, making the system unresponsive and unable to behave according to its specifications. For example, if the NullPointerException is not caught, the error provokes a failure: the system responds to any request with a 500 response.
    
    NOTE: Fault becomes an error which will turn out failure. Need to build fault-tolerant system,elf-repairing or self-healing system -  An essential part of resilience is ensuring that a failure will not cascade to other components of the system but stay isolated while it gets fixed. Cloud can provide that.
    Patterns like circuit breakers, retries, timeouts, and rate limiters will help.

  ## Observability 
  Control theory - observability is a measure of how well you can infer its internal state from its external outputs.
  s/w - single app or distributed app
  external o/p - metrics,logs, traces
  Four pillars - 
  * Monitoring - Monitoring is about measuring specific aspects of an application to get information on its overall health and identify failures. Spring boot actuator and Prometheus expose metrics
  * Alerting/Visualization
  * Distributed Tracing
  * Log Aggregation/analytics
 ## Manageability 
 In control theory, the counterpart of observability is controllability—the ability of external input to change the state or the output of a system in a finite time interval. manageability measures how easily and efficiently an external input can change the state or the output of a system. In s/w, it’s the ability to modify an application’s behavior without needing to change its code.
  Aspects -
  * deploying and updating applications while keeping the overall system up and running
  * element is a configuration
  * Manageability is not only about particular changes themselves but also about how easily and efficiently you can apply those changes. essential to design applications that can adapt to changing requirements regarding functionality, the environment, and security. due to this, we should manage the system through automation.
 NOTE: maintainability - which measures how easily and efficiently you can change a system from the inside by changing its code.
# Cloud native Practices
## Automation
 * core tenet of cloud-native
 * eliminate manual repetitive tasks and make the system stable and reliable.
 * eliminate unstable, unreliable snowflake servers. snowflake server - When each server is provisioned, managed, and configured manually
 * provide immutable servers - all tasks acting on those servers are automated, every change can be tracked in source control, reducing  risks, and each setup is reproducible
 * Cloud providing an automated self-service model for resources.
 * Two significant categories of automation are -
     2. infrastructure provisioning (infra-as-a-code) - terraform tools provision vm with Ubuntu
     3. configuration management ( config-as-a-code) - ansible installs java and other runtimes inside Ubuntu 
 NOTE: “pets vs. cattle”
 when comparing traditional snowflake infrastructure (requiring a lot of care and attention, like pets) and immutable infrastructure or containers (characterized by being disposable and replaceable, like cattle)
Let's say ubuntu 20.4 -> 22.04 upgrade, two options
1. perform on existing server(phoenix server) with automation scripts
2. start new server (immutable) with ubuntu 22.04 and other version retired.
  ## Continuous Delivery 
  *a software development discipline where you build software in such a way that the software can be released to production at any time*
  which can have a shorter feature cycle and  “make high-impact changes frequently and predictably with minimal toil,” - CNCF
  * Continuous delivery encourages the automation of the whole process via a deployment pipeline (also called a continuous delivery pipeline).
  * continuous delivery vs continuous deployment - The former approach makes sure that after every change, the software is in a state in which it can be deployed to production. When that’s actually done is a business decision. With continuous deployment we add one last step to the deployment pipeline to automatically deploy a new release in production after every change.
  * Continuous delivery is not about tools. It’s a discipline that involves cultural and structural changes in your organization.
  * CI/CD - continuous integration is not the only practice included in the continuous delivery discipline. For example, test-driven development (TDD), automated configuration management, acceptance testing, and continuous learning are equally important.
    ## Devops
    * A culture where people, regardless of title or background, work together to imagine, develop, deploy, and operate a system.
    * DevOps is a culture, and it’s all about working together toward a common goal. Developers, testers, operators, security experts, and other people, regardless of title or background, work together to bring ideas to production and produce value.
    * No more silos - “You build it, you run it.”
      Myth -
      * DevOps doesn’t mean NoOps.- Mistake that developer will take ops role and ops role go away. its collaboration. A team includes both roles with the overall skills required to build a product from idea to production.
      * DevOps is not a tool. - it is about culture. You don’t turn into a DevOps organization by using particular tools.DevOps is not a product, but tools are relevant enablers.
      * DevOps is not automation. Even if automation is an essential part of DevOps, automation is not its definition. DevOps is about developers and operators working together from the original idea to production while possibly automating some of their processes, such as continuous delivery.
      * DevOps is not a role. - If we consider DevOps to be a culture or a mindset, it’s hard to make sense of a DevOps role. And yet, there is an increasing request for DevOps engineers. Usually, when recruiters search for DevOps engineers, they are looking for skills like proficiency with automation tools, scripting, and IT systems.
      * DevOps is not a team.- Organizations not fully understanding the preceding points risk keeping the same silos as before, with one change: replacing the Ops silo with a DevOps silo, or, even worse, simply adding a new DevOps silo.
    # Cloud native computing models
    Containers (managed by orchestrators) and serverless
    ## Containers
    * Virtualization works by leveraging a hypervisor component that abstracts the hardware.making it possible to run multiple operating systems on the same machine in an isolated fashion.
    * containers enable agility, portability across different environments, and deployment repeatability
    * hypervisor would run directly on the machine hardware (type 1) or on the host operating system (type 2)
    * OS container is a lightweight executable package that includes everything needed to run the application.
    * Containers share the same kernel as the host: there’s no need to bootstrap full operating systems to add new isolated contexts.
    * On Linux, that is possible by leveraging a couple of features offered by the Linux kernel:

        **namespaces** for partitioning resources among processes so that each process (or group of processes) can only see a subset of the resources available on the machine

         **cgroups** for controlling and limiting the resource usage for a process (or group of processes)
      NOTE: When using virtualization only, the hardware is shared. whereas containers also share the same operating system kernel

      NOTE : OS container is a method for running one or more processes in an environment isolated from the rest of the system.

    ## Serverless
      * Serverless applications are typically event-driven and run only when there is an event to handle, such as an HTTP request or a message.
      * Function as a Service (FaaS) - applications are stateless, triggered by events, and fully managed by the platform
        vendor platform - AWS Lambda, Azure Functions, or Google Cloud Functions
        open source platform -  Knative and Apache OpenWhisk
#Architectures for cloud native applications
 
 
