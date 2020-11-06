
transtats.org

# Transtats Test Automation
> Last Updated 4th November 2020

## OVERVIEW
Transtats is a web application which talks to several services to fetch and analyse translation data and create helpful representations. In addition to this, it can help set up workflow automation. To assure correct results in production loads, a thorough test cycle is absolutely necessary.

## GOALS
- Identify test methods and their requirements in Transtats context.
- Work on feasibility towards test automation by prioritizing.
- Set up a sustainable test infrastructure to assure accuracy of even minor details.
- Ensure quality of Transtats releases along with their limitations.
- Channelize testing processes to improve reliability.

## SPECIFICATIONS
This is an effort to create a robust test environment. A combined set of tools and applications which may meet requirements of respective test methods. Moreover, there must be room for continuous improvement. Tests may majorly cover integration, functional and release.

## TEST METHODS
### Unit Tests
Code to test functional code units, usually by mocking external resources. These can be atomic and integrated with CI. (_in GitHub itself_) Transtats is very poor in unit tests and hence require attention. This could be written using [unittest]( https://docs.python.org/3/library/unittest.html) in python and kept in the main source [repository]( https://github.com/transtats/transtats). Though writing unit tests are easy, they can be extremely time consuming.

### Integration Tests
Code to test functional code units as a group by creating test external resources (_stubs_), which behaves the similar way. A few examples in Transtats are [here]( https://github.com/transtats/transtats/tree/devel/dashboard/tests). Test database is created and loaded with test data. External services and message queues are mocked. [CircleCI]( https://app.circleci.com/pipelines/github/transtats) are being used for running these tests. Though we have a few integration tests, the coverage is still poor and hence needs attention. Similar to unit tests, they can reside in the main repository and writing integration tests can be time consuming too.

### Functional Tests
Transtats is growing by adding a lot of new features and workflows. Testing these workflows are part of release testing (_as of now_) and are manual. An effort towards automating this is [here]( https://github.com/transtats/test-automation).

- Identification of workflows and creating test data may prove to be helpful.
- Another important aspect is UI interface testing using something like selenium or [quickstrom]( https://docs.quickstrom.io/index.html).

Testing of workflows by loading different sets of test data is the basis here. For example, running translation platform sync for 4 packages, each pointing to different: damned-lies, transifex, weblate, zanata. Or running build system sync for a package being tracked for both fedora and RHEL. These permutations/combinations need to be identified.

Certainly this may require a lot of effort, great if folks join hands!

### Performance Tests
Web applications should always be tested for performance under different circumstances. Monitoring and profiling are two aspects that should be considered. For example, turn around time to load the ‘Package List’ page with 10, 100, 200, 400, 800 packages.

- Does it change with more resources added?
- Is there an impact with a remote database (SIN, Tokyo)?

API load testing using tools like JMeter could also be meaningful. For example, to determine when Transtats exhaust? The limitation.

This may not seem urgent, however, always good to get measured.

### Deployment Tests
Transtats is being distributed and deployed using several tools, platforms. In RHEL we have ansible [scripts]( https://github.com/transtats/transtats-ansible) to deploy on vm(s) hosted in OpenStack platform. Whereas, in fedora Transtats is deployed using OpenShift v3. It is also built for docker [images]( https://hub.docker.com/r/transtats/transtats). Furthermore, the devel environment is recommended using vagrant. This is also a part of release testing. However, to keep ever-ready Transtats - this should be part of the pipeline.

### Responsive Web Design Tests
Testing web interfaces for UI consistency

- On different web browsers, platforms: win, linux, mac
- For different resolutions: desktop, mobile 

## ACTION ITEMS
- Identify requirements for each method.
    - Choosing appropriate tools, scripts, apps, workflow.
- Analyse feasibility and respective desired outcome.
- Deducing priority, and schedule their execution.
- Pushing their test reports to a common dashboard.
    - A basic check before we make a release.

