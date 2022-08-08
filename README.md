# About This Repository

This repository would not directly receive any codes from contributors of `tarun-service` and `tarun-frontend`. This is an automated assembled repository that tracks the software releases, bug-fixes and nightly developments for **Tarun Mail**. The only code that would be directly submitted to this repository would be `devOps` related automation codes.

### The problem

**Tarun** is a single piece of software that provides mail related functionality to its end users. However, this application is actually a composition of two very different lines of development viz., `front-end cross platform client` and `back-end service`. As such, they both require independent lines of development and testing. Currently, **GIT** does not have a mechanism to auto-combine release branches from two different repositories, integrate them, test them and create installable release bumndles for various platforms.

Therefore a little bit of `devOps` magic is needed to be able to do that.

### How does it work?

Each platform viz., MacOS, Linux and Windows has a different method for allowing sharing and/or discovery of executables. Through some coded automation systems, the release branches of `tarun-service` and `tarun-frontend` would be pulled into the current `pre-release` branch of this repository. 

[Tests](#testing) would be run on the combined codebase and if all tests pass, the release would be tagged and [a new release would be created](#release-automation). This new release would then go through the [Release Automation Process](#release-automation) and the resulting installable bundles would be uploaded to the respective test platforms. 

Further upon more automated testing of these individual bundles, the release would be marked as `stable` and the installable bundles would be uploaded to the respective platforms' app stores or whatever other release methods we would support. This step would commence the [Beta](#beta-testing) testing phase. Upon further approval of this phase, the release would be marked as `production` and the installable bundles would now be marked as a new version.

### Testing

This repository would have a set of *three* testing strategies: 

    1. Unit Testing
    2. Integration Testing
    3. Benchmarking

Every test function needs to have complete documentation and a clear description of what it is testing. The test functions would be written in such a way that they would be able to test the `tarun-service` and `tarun-frontend` codebases independently.

#### Unit Testing

The unit tests for this project would be set in stone between each major version i.e. `v1.0.0` through `v1.9.9` shall not see any changes in the unit tests. There maybe additional tests but old tests cannot be removed or modified.

Additionally the following points should be noted:

    1. Unit tests should not call any external servcies. 
    2. Unit tests should not call any database connections. All database connections shall be mocked.
    3. There has to be a minimum code coverage of 85% for contribution or acceptance.
    4. No unit test shall share state with any other unit test. Each unit test should be independent of any other unit test. And they should be able to run parallely.


#### Integration Testing

The integration tests for this project would be set in stone between each major version i.e. `v1.0.0` through `v1.9.9` shall not see any changes in the integration tests. There maybe additional tests but old tests cannot be removed or modified.

Additionally the following points should be noted:

    1. Integration tests can call external services only through provided interfaces/implementations/providers.
    2. Integration tests should not have connections/access credentials hard-coded. They should be able to read configuration from a file or environment variables.
    3. Integration tests would be run from one of two viewpoints viz., `tarun-service` and `tarun-frontend`. 


#### Benchmarking

The benchmarking tests for this project would be set in due course. The acceptable parameters for this suite of tests should focus on measuring usability and performance of the application. The tests should be able to run on a variety of hardware configurations and should be able to report the results in a human readable format. No release would be approved without passing this suite of tests.

The benchmarking tests would be run on the `pre-release` branch of this repository. This would test the backend and frontend as a whole. The results of this test would be used to determine the `stable` release.


### Release Automation

This repository would have a set of tools that would be deeply integrated with a CI server. The CI server would be responsible for running the tests and creating the release bundles. The CI server would also be responsible for running the [Benchmarking](#benchmarking) tests and reporting the results.

Once an acceptable release has been marked, the following steps should be accomplished:

    1. The release should be tagged with the version number.
    2. An executable or installable bundle should be created for *each* platform.
    3. These bundles then should be picked by the CI server and uploaded to the respective platforms.
    4. Once uploaded, these bundles should then be run/installed in the target system while logging performance and usability metrics.
    5. A suite of tests should then be run on the target system to determine if the release is stable or not.


### Beta Testing

The beta testing phase would be a manual process. The beta testers would be able to download the installable bundles from the respective platforms. They would then be able to install the application and test it. The beta testers would be able to report bugs and feature requests. The beta testers would also be able to provide feedback on the performance and usability of the application.

Once the `beta testing phase` is over, the following should occur:

    1. The CI server should then create a `release` at `Github`.
    2. The CI server should then open an `issue` at `JIRA` for approval before submission to `app stores`.
    3. Once approved, this version should be submitted with the relevant information.
    4. This update should be marked at `JIRA` by the CI server.


### Supportted Platforms

Initially, the following platforms would be supported:

    1. MacOS
    2. Linux
    3. Windows