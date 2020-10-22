# 12-factor app

## Wut

Human expectations to software-as-a-service product interation.

## Why

Like emotions incept words, the Pain incept rules. The subj is a context for CI/CD, containerization, hot-update, development workflows, fast interaction dev/admin onboarding, etc.

## Where

https://12factor.net/

## TL;DR + advices

 To achive the unificated usage of the portable and easy scaling-up SaaS with easy deployment on different cloud platforms use declarative formats for setups, clean contact with OS.

1. **Codebase**
  * One codebase tracked in revision control and many deploys,
  * One codebase per one app or lib
  * There may be different workflow for each deploy (podaction, staging, dev1, dev2...)
2. **Dependencies**
  * Explicitly declare and isolate dependencies,
  * A twelve-factor app never relies on implicit existence of system-wide packages,
  * *Dependency declaration manifest* uses a *dependency isolation tool* during execution to ensure that no implicit dependencies “leak in” from the surrounding system: pip & Virtualenv (Python), autoconf/cmake & static linking (C/C++),
  * If the app needs to shell out to a system tool, that tool should be vendored into the app.
3. **Config**
  * Store config in the environment,
  * 12f-app requires strict separation of config from code,
  * Static configuration - static constants in src,
  * Dynaminc configuration - changes between deploys to use app with purpose,
  * If app uses config file, it does it explicitly (create default if not exists + report), and file uses well known format, and each position is commented,
  * 12f-app stores config in environment variables as they are easy to change unlike config files, execution platform-specific properties, etc.
  * Env vars should be granular, as the deploy may has it's own set of them,
  * If app is configured by config file, you may provide entry point for docker container with a script for translation the env vars into config.
4. Backing services
  * Treat backing services as attached resources
  * The code for 12f-app makes no distinction between local and third party services, attaching via config
  * Swith between one db/metrics/api/etc to another without any changes to the app's code,
  * Resources can be attached to and detached from deploys at will.
5. Build, release, run
  * Strictly separate build and run stages
  * Use pipelines
  * Pass artifacts from stage to stage
  * Any change must create a new release, and versioning strategy reflects how many chages should be applied to the environment to update 12f-app.
6. Processes
  * Execute the app as one or more stateless processes
  * 12f-app processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service, typically a database.
7. Port binding
  * Export services via port binding
  * 12f-app is completely self-contained
  * 12f-app exports HTTP as a service by binding to a port
  * Note also that the port-binding approach means that one app can become the backing service for another app, by providing the URL to the backing app as a resource handle in the config for the consuming app.
8. Concurrency
  * Scale out via the process model
  * 12f-app processes are a first class citizen. 
  * The share-nothing, horizontally partitionable nature of twelve-factor app processes means that adding more concurrency is a simple and reliable operation,
  * 12f-app processes should never daemonize or write PID files. Instead, rely on the operating system’s process manager 
9. Disposability
  * Maximize robustness with fast startup and graceful shutdown
  * 12f-app’s processes are disposable, meaning they can be started or stopped at a moment’s notice
  * Processes shut down gracefully when they receive a SIGTERM signal from the process manager,
  * Processes should also be robust against sudden death, in the case of a failure in the underlying hardware.
10. Dev/prod parity
  * Keep development, staging, and production as similar as possible
  * 12f-app's developer resists the urge to use different backing services between development and production,
  * 12f-app is designed for continuous deployment by keeping the gap between development and production small. 
11. Logs
  * Treat logs as event streams
  * 12f-app never concerns itself with routing or storage of its output stream
  * If app doesn't see the env var is set, it explicitly reports about using default value.
  * If app is well-configured, it reports the status explicitly
12. Admin processes
  * Run admin/management tasks as one-off processes 
  * Running database migrations, running console to run arbitrary code or inspect the app’s models against the live database, running one-time scripts committed into the app’s repo: one-off admin processes should be run in an identical environment as the regular long-running processes of the app. They run against a release, using the same codebase and config as any process run against that release. Admin code must ship with application code to avoid synchronization issues.