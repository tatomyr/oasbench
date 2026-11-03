# OpenAPI Linter Race

[![Last race](https://img.shields.io/github/last-commit/tatomyr/oasbench/main?path=results&label=last%20race)](https://github.com/tatomyr/oasbench/actions/workflows/benchmark.yml)
[![Race status](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Frepos%2Ftatomyr%2Foasbench%2Factions%2Fworkflows%2Fbenchmark.yml%2Fruns%3Fper_page%3D1&query=%24.workflow_runs%5B0%5D.status&label=race)](https://github.com/tatomyr/oasbench/actions/workflows/benchmark.yml)

Speed benchmark of OpenAPI linters on public API descriptions.
Every linter runs at its latest release (Redocly CLI also at its latest snapshot) with its default ruleset; Spectral has none, so it gets [`.spectral.yaml`](.spectral.yaml), which extends `spectral:oas`.

## Results

<!-- BENCHMARK:START -->
Generated 2026-11-03 17:15 UTC by [this workflow run](https://github.com/tatomyr/oasbench/actions/runs/41682365921) on AMD EPYC 9V45 96-Core Processor, 4 cores, 15 GB RAM, Linux 7.0.0-1017-azure, Node v24.22.1.
Each command ran 5 times, one after another, after a 5 s pause; the time is wall-clock from process start to exit, as `time` reports it, and the table shows the median. A command that did not finish within 5 minutes was killed and not repeated. ☠️ marks a command that was killed or crashed. 🐎 marks the fastest tool for each API description, and 🐌 the slowest.

| Median lint time, s | Azure Compute<br><small>205 ops<br>2.3 MB</small> | Stripe<br><small>612 ops<br>6.3 MB</small> | DigitalOcean<br><small>884 ops<br>4.2 MB</small> | AWS EC2<br><small>1188 ops<br>5.6 MB</small> | GitHub<br><small>1254 ops<br>10.7 MB</small> | Cloudflare<br><small>3763 ops<br>20.4 MB</small> |
| --- | :---: | :---: | :---: | :---: | :---: | :---: |
| **redocly**<br><small>v0.0.0-snapshot.1793725129</small> | <br>[0.89](results/azure/redocly.1.txt) | 🐎<br>[1.33](results/stripe/redocly.1.txt) | <br>[2.08](results/digitalocean/redocly.1.txt) | <br>[1.77](results/aws-ec2/redocly.1.txt) | 🐎<br>[3.19](results/github/redocly.1.txt) | <br>[5.57](results/cloudflare/redocly.1.txt) |
| **redocly-latest**<br><small>v2.73.0</small> | <br>[0.86](results/azure/redocly-latest.1.txt) | <br>[1.35](results/stripe/redocly-latest.1.txt) | <br>[2.12](results/digitalocean/redocly-latest.1.txt) | 🐎<br>[1.75](results/aws-ec2/redocly-latest.1.txt) | <br>[3.31](results/github/redocly-latest.1.txt) | 🐎<br>[5.50](results/cloudflare/redocly-latest.1.txt) |
| **vacuum**<br><small>v0.36.2</small> | 🐎<br>[0.33](results/azure/vacuum.1.txt) | <br>[1.87](results/stripe/vacuum.1.txt) | <br>[2.91](results/digitalocean/vacuum.1.txt) | <br>[2.49](results/aws-ec2/vacuum.1.txt) | <br>[5.75](results/github/vacuum.1.txt) | <br>[7.56](results/cloudflare/vacuum.1.txt) |
| **speakeasy**<br><small>v1.806.0</small> | <br>[0.41](results/azure/speakeasy.1.txt) | <br>[2.99](results/stripe/speakeasy.1.txt) | 🐎<br>[1.62](results/digitalocean/speakeasy.1.txt) | 🐌<br>[7.85](results/aws-ec2/speakeasy.1.txt) | <br>[5.85](results/github/speakeasy.1.txt) | <br>[10.15](results/cloudflare/speakeasy.1.txt) |
| **spectral**<br><small>v6.17.0</small> | <br>[2.50](results/azure/spectral.1.txt) | 🐌<br>[11.91](results/stripe/spectral.1.txt) | <br>[23.62](results/digitalocean/spectral.1.txt) | <br>[5.41](results/aws-ec2/spectral.1.txt) | 🐌<br>[35.86](results/github/spectral.1.txt) | 🐌<br>[61.15](results/cloudflare/spectral.1.txt) |
| **scalar**<br><small>v2.13.2</small> | 🐌<br>[13.03](results/azure/scalar.1.txt) | ☠️<br>[58.11](results/stripe/scalar.1.txt) | 🐌<br>[165.27](results/digitalocean/scalar.1.txt) | ☠️<br>[300.06](results/aws-ec2/scalar.1.txt) | ☠️<br>[300.10](results/github/scalar.1.txt) | ☠️<br>[300.16](results/cloudflare/scalar.1.txt) |
<!-- BENCHMARK:END -->

## OpenAPI Descriptions

The [workflow](.github/workflows/benchmark.yml) downloads the latest version of each source and bundles it into one file in `openapi/` with `redocly bundle`:

- [Azure Compute](https://github.com/Azure/azure-rest-api-specs/tree/main/specification/compute/resource-manager/Microsoft.Compute/Compute/stable/2026-04-01) (Swagger 2.0, MIT)
- [Stripe](https://github.com/stripe/openapi/blob/master/openapi/spec3.yaml) (MIT)
- [DigitalOcean](https://github.com/digitalocean/openapi/tree/main/specification) (Apache-2.0)
- [AWS EC2](https://github.com/APIs-guru/openapi-directory/blob/main/APIs/amazonaws.com/ec2/2016-11-15/openapi.yaml) (CC0-1.0, converted from the AWS SDK model by APIs.guru)
- [GitHub](https://github.com/github/rest-api-description/blob/main/descriptions/api.github.com/api.github.com.yaml) (MIT)
- [Cloudflare](https://github.com/cloudflare/api-schemas/blob/main/openapi.yaml) (BSD-3-Clause)

