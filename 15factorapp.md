# 12-Factor methodology
* Best practice and development patterns
# One codebase, one application
* one codebase for each application
* shared code should be made as the library or deployed as a separate standalone model and act as a backend service
* deployment is running instances of apps. diff deployment on different environments. any aspect that changes between env like config should be kept outside the codebase.
# API First
* cloud-native system is usually made up of different services that communicate through APIs
* API first approach while designing a cloud-native application encourages you to think about fitting it into a distributed system and favors the
  distribution of the work across different teams.
# Dependency management
* dependencies should be declared explicitly in a manifest and be available for the dependency manager to download from a central repository.
* Maven and Gradle pom or build
# Design, build, release, run
 * Design stage - Technologies, dependencies, and tools needed by a specific application feature are decided.
 * Build - The codebase is compiled and packaged together with its dependencies as an immutable artifact called a build. The build artifact must be uniquely identified.
 * Release stage - The build is combined with a specific configuration for the deployment. Each release is immutable and should be uniquely identifiable, such as by using semantic versioning (for example, 3.9.4) or a timestamp (for example, 2022-07-07_17:21). Releases should be stored in a central repository for easy access, like when a rollback to a previous version is required.
 * Run stage - The application runs in the execution environment from a specific release.
   NOTE: The 15-factor methodology requires a strict separation of these stages and doesn’t allow changes to the code at runtime, since that would result in a mismatch with the build stage. The build and release artifacts should be immutable and labeled with a unique identifier to guarantee reproducibility.
# Configuration, credentials, and code
* don't store in codebase.
* change configuration without building code.
* preferable to the environment variable.
* some default configurations can kept in codebase.
 # Logs 
 * Applications should log to the standard output, treating logs as events emitted in a sequence ordered by time.
 * external tool (a log aggregator) will fetch, collect, and make logs available for inspection.
 # Disposability 
 * application is disposable if it can be started or stopped at any time.
 * fast startup enables the elasticity of the system, ensuring robustness and resilience. Without a fast startup, you will have performance and availability issues.
 * graceful shutdown is when an application, on receiving a signal to terminate, stops accepting new requests, completes the ones already in progress, and finally exits
 # Backing services
 * Backing services can be defined as external resources that an application uses to deliver its functionality.
 * backing services are databases, message brokers, caching systems, SMTP servers, FTP servers, or RESTful web services.
 * Treating them as attached resources means that you can easily change them without modifying the application code.can use a different service depending on the environment. For example, resource binding for a database could consist of a URL, a username, and a password.
  # Environment parity
  * Keep all your environments as similar as possible.
  In reality, there are three gaps that this factor tries to address
     1. Time gap - code change and deployment gaps. promote automation and Continous deployment.
     2. people gap - dev and ops gaps. DevOps culture.
     3. tools gap - tool diff between env. like dev db is H2 and prod is PostgreSQL. Try to use the same db for all env.
  # Administrative processes
  * Some management tasks are usually needed to support applications
  * Tasks like database migrations, batch jobs, or maintenance jobs should be treated as one-off processes.
  * application processes and the code for administrative tasks should be tracked in revision control, delivered with the application they support, and executed in the same environment as the application.
  * It’s usually a good idea to frame administrative tasks as small standalone services that run once and then are thrown away or as functions configured in a stateless platform to be triggered when certain events happen, or you can embed them in the application itself, activating them by calling a specific endpoint.
  # Port binding 
  * The app should be self-contained and export its services via port binding.
  * The application is self-contained if it doesn’t depend on an external server in the execution environment.
  * Spring Boot, for example, lets you use an embedded server . no need for external tomcat installations.
  * one-to-one mapping between application and server, a traditional method where multiple applications are deployed to the same server
  * dynamic port binding
  # Stateless processes
  * To ensure scalablity, share-nothing architecture is required -  no state should be shared among different application instances
  * Ask yourself if any data would be lost should an instance of your application be destroyed and recreated. If the answer is affirmative, then your application is not stateless.
  *  stateless application delegates the state management and storage to a backing service.
  # Concurrency
  * processes as first-class citizens
  *  horizontally scalable, distributing the workload across many processes on different machines, and this concurrent processing is only possible if the applications are stateless
  *  Processes can be classified according to their types. For example, you might have web processes that handle HTTP requests and worker processes that execute scheduled jobs in the background.
  # Telemetry
  * telemetry data are logs, metrics, traces, health status, and events
  * TREAT APPS LIKE SPACE PROBES
      I like to think of pushing applications to the cloud as launching a scientific instrument into space.
   * monitoring your application means -
         Application performance monitoring (APM) -  streams on events that capture and present to generic dashboard 
         Domain-specific telemetry - busniess domain specific events streams and generate analytics & reporting.often feed to big data system - warehouse,analysis and forecasting.
     NOTE APM vs Domain specific telemetry - APM might provide you the average number of HTTP requests per second an application is processing, while domain-specific telemetry might tell you the number of widgets sold to people on iPads within the last 20 minutes.
         Health and system logs - something that should be provided by your cloud provider. They make up a stream of events, such as application start, shutdown, scaling, web request tracing, and the results of periodic health checks.
     * cloud make monitoring and telemetry are still difficult, probably even more difficult than traditional as stream contains lots of combination of data.
     * planning your monitoring strategy , consider -
          how much information you’ll be aggregating
          rate at which it comes in
          how much of it you’re going to store
          Auditing and monitoring cloud applications spl prod is important.
# Authentication and authorization
* Security should never be an afterthought.
* enable audit trail - who accessed what and when
* all cloud-native applications would secure all of their endpoints with RBAC (role-based access control)
* use OAuth2, OpenID Connect, various SSO servers and standards
