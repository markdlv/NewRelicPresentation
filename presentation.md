[Node.js agent documentation intro](https://docs.newrelic.com/docs/agents/nodejs-agent/getting-started/introduction-new-relic-nodejs)

HSLIDE

Best documentation pages

* [Node.js agent API](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/nodejs-agent-api)
    * Defaults record quite a bit
* [Node VM measurements](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/node-vm-measurements)
    * These show up as *metrics* in the Insights section
* [Node.js custom metrics](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/nodejs-custom-metrics)
* [Node.js custom instrumentation](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/nodejs-custom-instrumentation)
* [Page load timing](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/page-load-timing-nodejs)

NOTE: For Node.js agent API - we can decorate current transactions with custom parameters!

HSLIDE

Quick overview of how newrelic starts up
* Looks in ```NEW_RELIC_HOME``` *directory* for newrelic.js file
* Simply ```require```ing newrelic module starts the process
    * Therefore, avoid it if you *don't* want to report to newrelic:
    ```
        let newrelic;

        if (process.env.NEW_RELIC_HOME && process.env.NO_NEW_RELIC_USAGE !== 'true') {
            newrelic = require('newrelic');
        }
    ```

VSLIDE

Configuration methods and precedence
![new relic config overrides](https://docs.newrelic.com/sites/default/files/styles/inline_660px/public/thumbnails/image/nodejs%20config%20cascade_0.png?itok=r_yPD--g)

* NOTE: some properties only have an config-file option

VSLIDE

On an EC2 instance:
* [base AMI file](https://bitbucket.org/inindca/ansible-base/src/680cce1c1b7daf162044f7d3fab48eac643fd2b5/base/roles/newrelicnode-configure/templates/newrelic-config.js.j2?at=master&fileviewer=file-view-default)
* Written to / read from [/opt/](https://bitbucket.org/inindca/billing-service/raw/a1a3e5b94d90abbb8c13200f66b262786d818ac2/packer-ansible/ansible/ininservice/roles/billing-configure/templates/billing-supervisord.ini.j2)
* Add [environment variables](https://bitbucket.org/inindca/subscription-service/raw/612fec79d7e2aee03806fa6d8a1af4b69d31c847/packer-ansible/ansible/ininservice/roles/subscription-configure/templates/subscription-supervisord.ini.j2) to override

NOTE: That base AMI file is for all node services, so make sure to put lots of team leads on any PR.

HSLIDE

Program against our interfaces (in SDC)
* [ServiceMetricsReporter](https://bitbucket.org/inindca/billing-service/src/9897519d189aa0e1e8ece1f8bce10d2bccdde2ec/src/AppDependencyBuilder.js?at=master&fileviewer=file-view-default#AppDependencyBuilder.js-1038)
* [ServiceInstrumentor](https://bitbucket.org/inindca/billing-service/src/9897519d189aa0e1e8ece1f8bce10d2bccdde2ec/src/interop/zuora/ZuoraBillingHandler.js?fileviewer=file-view-default#ZuoraBillingHandler.js-761)

NOTE: How can we integrate further?

HSLIDE

* [Setup local machine](https://bitbucket.org/inindca/service-delivery-common/src/c66f10c7ee73?at=master)
* Demo of testing a new metric or instrumentation
    * Note how [key transactions](https://docs.newrelic.com/docs/apm/transactions/key-transactions/introduction-key-transactions) work

HSLIDE

Finding a metric in New Relic
* Example: VM measurements (gc, memory, cpu)
* Example: our custom metric

VSLIDE

Finding a custom event
* Example: our custom event

HSLIDE

* Dream a bit about issues this might solve
    * More insight into who is using our APIs
    * Stats on billing jobs
    * Stats on invoicing
    * Stats on kafka message processing
    * Stats on kafka re-balance
* Finally: [Insights dashboards](https://insights.newrelic.com/accounts/864720/dashboards/273773)

NOTE: In order: addCustomParameters, recordEvent, recordEvent, recordMetric, incrementMetric). For billing jobs, both from a system/service health perspective, but possibly also just from an interest perspective.  For example, I'd be curious to see things like average user count, counts for concurrent vs. configured orgs, etc.

HSLIDE

Thanks!

Questions?

NOTE: Mainly, I just want to encourage us to continue integrating with NewRelic.  We've got some new tools to do that with the ServiceInstrumentor, but I know the main battle has been just being *aware* of the features.