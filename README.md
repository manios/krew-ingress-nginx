# krew-ingress-nginx

[![GitHub license](https://img.shields.io/github/license/kubernetes/ingress-nginx.svg)](https://github.com/kubernetes/ingress-nginx/blob/main/LICENSE)
[![GitHub Downloads (all assets, latest release)](https://img.shields.io/github/downloads/manios/krew-ingress-nginx/latest/total)](https://github.com/manios/krew-ingress-nginx/releases/tag/v1.11.2)
[![GitHub Repo stars](https://img.shields.io/github/stars/manios/krew-ingress-nginx)](https://github.com/manios/krew-ingress-nginx/stargazers)

## Overview

A custom [krew plugin index](https://krew.sigs.k8s.io/docs/developer-guide/custom-indexes/) that offers the latest version of [ingress-nginx kubectl plugin](https://kubernetes.github.io/ingress-nginx/kubectl-plugin/). Currently the official kubectl plugin cannot be installed due to the fact that it is on a very old version (`v0.31.0`) and throws an error described in [issue #12226](https://github.com/kubernetes/ingress-nginx/issues/12226). This repository provides a temporary workaround by offering custom builds of the plugin.

## Install

In order to install the plugin through this custom index , first of all you have to add this custom index:

```bash
kubectl krew index add ingress-manios https://github.com/manios/krew-ingress-nginx.git
```

And then install the plugin:

```bash
kubectl krew install ingress-manios/ingress-nginx-cm 
```

Then you can use it with `kubectl ingress-nginx-cm`.

**NOTE**: We had to add the `-cm` suffix in the plugin name in order for krew not to throw an error with the existing official plugin.

## Uninstall

To uninstall the plugin run:

```bash
kubectl krew uninstall ingress-nginx-cm
```

You can also remove the index with:

```bash
kubectl krew index remove ingress-manios
```

## Changelog

See [the list of releases](https://github.com/manios/krew-ingress-nginx/releases) for all changes.

### Supported Versions table

We will try to keep up with the [official supported versions](https://github.com/kubernetes/ingress-nginx/releases) of the ingress-nginx project.

| Supported | Ingress-NGINX version | k8s supported version        |
|-----------|-----------------------|------------------------------|
| 🔄        | **v1.12.1**           | 1.32, 1.31, 1.30, 1.29, 1.28 |
| 🔄        | **v1.12.0**           | 1.32, 1.31, 1.30, 1.29, 1.28 |
| 🔄        | **v1.11.4**           | 1.30, 1.29, 1.28, 1.27, 1.26 |
| 🔄        | **v1.11.3**           | 1.30, 1.29, 1.28, 1.27, 1.26 |
| 🔄        | **v1.11.2**           | 1.30, 1.29, 1.28, 1.27, 1.26 |


## Disclaimer about security

Due to lack of time, we build the executables manually (see [build.md](https://github.com/manios/krew-ingress-nginx/blob/buildscripts/build.md)) and upload them into this repository [Releases page](https://github.com/manios/krew-ingress-nginx/releases). So, at the moment there is no automated CI pipeline, security checks or code scans. Contributions are welcome!
