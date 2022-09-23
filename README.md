# fluxcd-csm-powermax

This repository gives an example on how to deploy the [CSI Driver for PowerMax](https://github.com/dell/csi-powermax) and affiliated [CSM modules](https://github.com/dell/csm) with [Flux CD](https://fluxcd.io/).

The organization follows the below structure:
```
.
├── apps
│   ├── base
│   └── overlays
│       ├── cork-development
│       │   ├── dev-ns
│       │   └── prod-ns
│       └── cork-production
│           └── prod-ns
├── clusters
│   ├── cork-development
│   └── cork-production
└── infrastructure
    ├── cert-manager
    ├── csm-replication
    ├── external-snapshotter
    └── powermax
```


* `apps` ; contains the applications to be deployed on the clusters
  * we have different overlays per cluster
* `cluster` ; contains the cluster-specific fluxcd main configuration usually ; using Azure Arc, there is none needed
* `infrastructure` ; contains the deployments that are used to run the infrastructure services ; they are common to every cluster
  * `cert-manager` ; is a dependency of `powermax` reverse-proxy
  * `csm-replication` ; is a dependency of `powermax` to support SRDF replication
  * `external-snapshotter` ; is a dependency of `powermax` to snapshot
  * `powermax` ; contains the driver installation
