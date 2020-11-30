# accelerators


# Continuous Testing Checklist

## TOOLS, SCRIPTING AND OVERALL TEST CREATION
Support for both manual and automated testing
The provision of libraries and APIs to create “homegrown” tests using common DSLs.
Ability to activate commercial tools (such as Perfecto Mobile)
Support of JMeter and API tests (BlazeMeter)
The ability to create browser-based tests (Selenium Builder, BlazeMeter Chrome Plugin)
Support of Selenium and Appium tests (Sauce Labs)


## PROVISIONING & RESOURCES
The option to run the same sets of tests with different provisioning (i.e. a developer can run a module test from nbehind the firewall with local resources, and the same test can run in production from multiple geographical locations on the public cloud)
The ability to easily adopt a new provisioning scheme when a test configuration is executed in a different environment (e.g. Dev, CI, Pre-Prod, Post-Prod). These schemes should include:
 The developer’s laptop for debugging and troubleshooting
 A private cloud of resources available on-premise and protected behind the firewall
 A public cloud of unlimited resources available on multiple geographical locations
 Sufficient resources in the public and private cloud, enabling organizations to run multiple tests in parallel with zero time to test
 The option for users to define which OS and Browser combinations they want to execute the test against
 The ability to start testing as part of the CI process (i.e. Jenkins, Travis, TeamCity, CircleCI etc.)
 
## AUTOMATION
The ability to run any test configuration, a test, or a set of tests using simple API calls
The option to run as many tests as required in parallel
Availability of all test data via a REST API
 
## ON-DEMAND TESTING AND RE-RUNNING FAILED USE CASES
The ability to run any type of test on-demand. This is critical for test development, debugging, troubleshooting and identifying the root cause of a failure
The option to automate test executions and run the same test on-demand
 
## MODULES, BUILDS, RELEASE CANDIDATES, RELEASES AND PRODUCTION
The ability to combine different configuration fragments into one test configuration in order to comprehensively test build, release, and production snapshots.
 
## VERSION CONTROL FRIENDLY INCREMENTAL TESTING
The ability to support version control, incremental testing and associate test configurations, sets of tests, and tests with versions (e.g code, build, RC, releases).
 
## AUTOMATIC ‘FAILURE’ ALERTS
Automatic indications of failures, with an alerting scheme per developer, module and project
The ability to gather all test artifacts and immediately send to relevant people
The option to run the failed tests again to identify the root cause
 
## REPORTING
A seamless integration with existing reporting solutions (e.g. Jenkins Performance Trend)
The option to group tests by builds
The ability to give jobs a ‘pass’ or ‘fail’ status and group accordingly
Pass/fail trend reports
“Deep dive” reports for diagnostics and analysis, which can overlay data from third party systems (e.g. NewRelic, CloudWatch) for a comprehensive picture.
