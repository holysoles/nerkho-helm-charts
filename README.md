# Bluesky PDS Helm Chart

Helm chart for deploying a [Bluesky PDS](https://github.com/bluesky-social/pds) (Personal Data Server) on Kubernetes.

Forked from [Nerkho/helm-charts](https://github.com/Nerkho/helm-charts) with thanks to the original authors.

## Installing

```bash
helm repo add bluesky-pds https://holysoles.github.io/bluesky-pds-chart
helm install bluesky-pds bluesky-pds/bluesky-pds
```

Or install directly from the chart directory:

```bash
helm install bluesky-pds ./charts/bluesky-pds
```

## Configuration

See [charts/bluesky-pds/values.yaml](charts/bluesky-pds/values.yaml) for all configuration options.

## License
MIT - see [LICENSE](LICENSE)

- Much of the chart comes from the [Nerkho/helm-charts](https://github.com/Nerkho/helm-charts) project
- New commits (see git history) are also MIT licensed by this project
