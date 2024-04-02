# open-component-model common `pkg`
[![REUSE status](https://api.reuse.software/badge/github.com/open-component-model/pkg)](https://api.reuse.software/info/github.com/open-component-model/pkg)

This repository contains a collection of standard functionality to share amongst open-component-model repositories.

## Metrics

[metrics](./metrics) pkg contains a set of `MustRegister*` functions for registering Prometheus metrics.

The following is an example of usage for some gauges.

First, declare the metric for the controller under `metrics` package like this:

```go
// ComponentVersionReconciledTotal counts the number times a component version was reconciled.
// [component, version].
var ComponentVersionReconciledTotal = mh.MustRegisterCounterVec(
	"ocm_system",
	metricsComponent,
	"component_version_reconciled_total",
	"Number of times a component version was reconciled",
	"component", "version",
)
```

Notice, that the comment contains the parameters this metric needs in square brackets.

To use it in code, call:

```go
metrics.ComponentVersionReconciledTotal.WithLabelValues(cv.GetName(), cv.GetVersion()).Inc()
```

The `WithLabelValues` will correctly align the name and the version parameters. It will _panic_ if the values are
misaligned or not given correctly.

Certain constants are also defined in order to make all metrics uniform across the controllers.

## Support, Feedback, Contributing

This project is open to feature requests/suggestions, bug reports etc. via [GitHub issues](https://github.com/SAP/pkg/issues). Contribution and feedback are encouraged and always welcome. For more information about how to contribute, the project structure, as well as additional contribution information, see our [Contribution Guidelines](CONTRIBUTING.md).

## Code of Conduct

We as members, contributors, and leaders pledge to make participation in our community a harassment-free experience for everyone. By participating in this project, you agree to abide by its [Code of Conduct](CODE_OF_CONDUCT.md) at all times.

## Licensing

Copyright 2024 SAP SE or an SAP affiliate company and pkg contributors. Please see our [LICENSE](LICENSE) for copyright and license information. Detailed information, including third-party components and their licensing/copyright information, is available [via the REUSE tool](https://api.reuse.software/info/github.com/open-compopnent-model/pkg).
