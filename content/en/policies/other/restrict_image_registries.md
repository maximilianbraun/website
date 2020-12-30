---
type: "docs"
title: Restrict Image Registries
linkTitle: Restrict Image Registries
weight: 31
description: >
    Images from unknown registries may not be scanned and secured. Requiring use of known registries helps reduce threat exposure.
---

## Category
Workload Management

## Definition
[/other/restrict_image_registries.yaml](https://github.com/kyverno/policies/raw/main//other/restrict_image_registries.yaml)

```yaml
apiVersion : kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: restrict-image-registries
  annotations:
    policies.kyverno.io/category: Workload Management
    policies.kyverno.io/description: Images from unknown registries may not be scanned and secured. 
      Requiring use of known registries helps reduce threat exposure.
spec:
  validationFailureAction: audit
  rules:
  - name: validate-registries
    match:
      resources:
        kinds:
        - Pod
    validate:
      message: "Unknown image registry."
      pattern:
        spec:
          containers:
          - image: "k8s.gcr.io/* | gcr.io/*"

```