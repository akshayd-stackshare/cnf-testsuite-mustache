asdaa  aa # CNF Test Suite

| Main                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------- |
| [![Build Status](https://github.com/cncf/cnf-testsuite/workflows/Crystal%20Specs/badge.svg)](https://github.com/cncf/cnf-testsuite/actions) |

The CNF Test Suite is a tool that validates telco application's (i.e. [Cloud Native Network Functions - CNFs)](https://github.com/cncf/cnf-testsuite/blob/main/EXAMPLE-CNFS.md) adherence to [cloud native principles](https://networking.cloud-native-principles.org/) and best practices.

This Test Suite initiative works closely with the [CNF WG](cnf-wg/README.md) which determines requirements for the CNF Test Suite program.

## Installation and Usage

To get the CNF Test Suite up and running, see the [Installation Guide](INSTALL.md).

#### To give it a try immediately you can use these quick install steps

Prereqs: kubernetes cluster, wget, curl, helm 3.1.1 or greater on your system already.

1. Install the latest test suite binary: `source <(curl -s https://raw.githubusercontent.com/cncf/cnf-testsuite/main/curl_install.sh)`
2. Run `setup` to prepare the cnf-testsuite: `cnf-testsuite setup`
3. Pull down an example CNF configuration to try: `curl -o cnf-testsuite.yml https://raw.githubusercontent.com/cncf/cnf-testsuite/main/example-cnfs/coredns/cnf-testsuite.yml`
4. Initialize the test suite for using the CNF: `cnf-testsuite cnf_setup cnf-config=./cnf-testsuite.yml`
5. Run all of application/workload tests: `cnf-testsuite workload`

#### More Usage docs

Check out the [usage documentation](USAGE.md) for more info about invoking commands and logging.

## Cloud Native Categories

The CNF Test Suite will inspect CNFs for the following characteristics:

- **Configuration** - The CNF's configuration should be managed in a declarative manner, using ConfigMaps, Operators, or other declarative interfaces.
- **Compatibility, Installability & Upgradability** - CNFs should work with any Certified Kubernetes product and any CNI-compatible network that meet their functionality requirements while using standard, in-band deployment tools such as Helm (version 3) charts.
- **Microservice** - The CNF should be developed and delivered as a microservice.
- **State** - The CNF's state should be stored in a custom resource definition or a separate database (e.g. etcd) rather than requiring local storage. The CNF should also be resilient to node failure.
- **Reliability, Resilience & Availability** - CNFs should be reliable, resilient and available to failures inevitable in cloud environments. CNFs should be tested to ensure they are designed to deal with non-carrier-grade shared cloud HW/SW platforms.
- **Observability & Diagnostics** - CNFs should externalize their internal states in a way that supports metrics, tracing, and logging.
- **Security** - CNF containers should be isolated from one another and the host. CNFs are to be verified against any common CVE or other vulnerabilities.

See the [Test Categories Documentation](TEST-CATEGORIES.md) for a complete overview of the tests.

## Contributing

Welcome! We gladly accept contributions on new tests, example CNFs, updates to documentation, enhancements, bug reports, and more.

- [Contributing guide](CONTRIBUTING.md)
- [Good first issues](https://github.com/cncf/cnf-testsuite/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)

## Communication and community meetings

- Join the conversation on [CNCF's Slack](https://slack.cncf.io/) channels
  - [#cnf-testsuite](https://cloud-native.slack.com/archives/C01V28MLYEP)
  - [#cnf-testsuite-dev](https://cloud-native.slack.com/archives/C014TNCEX8R)
- Join the weekly Office Hours meeting

  - Meetings every Tuesday at 7:15am - 8am Pacific Time 
  - Meeting minutes are [here](https://docs.google.com/document/d/1IbrgjqIkOCvrrSG0DRE6X62UUZpBq-818Mn8q0nkkd0/edit)

- Join the weekly [CNF Working Group meeting](https://github.com/cncf/cnf-wg#recurring-meetings) on Mondays.

- Request an Intro to the CNF Certification [here](https://calendly.com/cnfcertification/intro)

## Presentations

**CNF Test Suite Demo**
- [Recording](https://drive.google.com/file/d/1SBHE5Dqx6Sa-m83WODbCEbbdiB2_l_U2/view?usp=sharing)
- [Slides](https://github.com/cncf/cnf-testsuite/files/6857515/SHARED-COMMON.CNF.Test.Suite.Demo.and.CNF.initiatives.overview.2021-06-29.pdf) (PDF)

**Crystal in the Cloud: A cloud native journey at Crystal 1.0 Conference**
- [Recording](https://youtu.be/n8g60VglyUw)
- [Slides](https://github.com/cncf/cnf-testsuite/files/6785788/Crystal.1.0.Crystal.in.the.Cloud_.CNF.Test.Suite.pdf) (PDF)


## Implementation overview

The CNF Test Suite leverages upstream tools such as [OPA Gatekeeper](https://github.com/open-policy-agent/gatekeeper), [Helm linter](https://github.com/helm/chart-testing), and [Promtool](https://prometheus.io/docs/prometheus/latest/configuration/unit_testing_rules/) for testing CNFs. The upstream tool installation, configuration, and versioning has been made repeatable.

The test framework and tests (using the upstream tools) are written in the human-readable, compiled language, [Crystal](https://crystal-lang.org/). Common capabilities like dependencies between tests and categories are supported.

Setup of vanilla upstream K8s on [Equinix Metal](https://metal.equinix.com/) is done with the [CNF Testbed](https://github.com/cncf/cnf-testbed/) platform tool chain, which includes [k8s-infra](https://github.com/crosscloudci/k8s-infra), [Kubespray](https://kubespray.io/). To add support for other providers, please submit a [Pull Request](https://github.com/cncf/cnf-testbed/pulls) to the [CNF Testbed](https://github.com/cncf/cnf-testbed/) repo.

## Code of Conduct

The CNF Test Suite community follows the [CNCF Code of Conduct](https://github.com/cncf/foundation/blob/main/code-of-conduct.md).

## License terms

The CNF Test Suite is available under the [Apache 2 license](LICENSE.md).
