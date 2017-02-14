[Node.js agent documentation intro](https://docs.newrelic.com/docs/agents/nodejs-agent/getting-started/introduction-new-relic-nodejs)

HSLIDE

Best documentation pages

* [Node.js agent API](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/nodejs-agent-api)
    * Get this automatically by requiring newrelic module
* [Node VM measurements](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/node-vm-measurements)
    * These show up as *metrics* in the Insights section
* [Node.js custom metrics](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/nodejs-custom-metrics)
* [Node.js custom instrumentation](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/nodejs-custom-instrumentation)
* [Page load timing](https://docs.newrelic.com/docs/agents/nodejs-agent/supported-features/page-load-timing-nodejs)

NOTE: we can decorate current transactions with custom parameters

HSLIDE

Program against our interfaces (in SDC)
* ServiceMetricsReporter
* ServiceInstrumentor

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

HSLIDE

* Demo of testing a new metric or instrumentation
* (Make sure this is already documented (outside this presentation, maybe in SDC since it will apply to all services?))

HSLIDE

Finding a metric in New Relic
* Example: VM measurements (gc, memory, cpu)
* Example: our custom metric

Finding a custom event
* Example: our custom event

HSLIDE

* Dream a bit about issues this might solve
* Show insights dashboards

HSLIDE

Questions?