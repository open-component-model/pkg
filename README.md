# open-component-model common `pkg`

> **Note:** This repository is scheduled for deprecation. Its only active consumer is [ocm-controller](https://github.com/open-component-model/ocm-controller).

This repository contains shared Go packages used by OCM Kubernetes controllers.

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

## Contributing

Contribution and feedback are encouraged and always welcome. For more information about how to contribute, see our [Contributing Guide](https://ocm.software/community/contributing/).

## Code of Conduct

OCM follows the [NeoNephos Code of Conduct](https://github.com/neonephos/.github/blob/main/CODE_OF_CONDUCT.md).

## Licensing

Please see our [LICENSE](LICENSE) for copyright and license information.
Detailed information including third-party components and their licensing/copyright information is available [via the REUSE tool](https://api.reuse.software/info/github.com/open-component-model/pkg).

---

<p align="center"><img alt="Bundesministerium für Wirtschaft und Energie (BMWE)-EU funding logo" src="https://apeirora.eu/assets/img/BMWK-EU.png" width="400"/></p>
