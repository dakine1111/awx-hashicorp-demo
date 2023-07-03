# Build Default execution environment with hvac
```bash
TAG='1.0.1'
podman build -t ee-supported-rhel8-vault:${TAG} .
oc login api.<YOUR_OCP>:6443 --insecure-skip-tls-verify=false -u <USERNAME>
HOST=$(oc get route default-route -n openshift-image-registry --template='{{ .spec.host }}')
podman login --tls-verify=false -u <USERNAME> -p $(oc whoami -t) $HOST
podman tag ee-supported-rhel8-vault:${TAG} ${HOST}/aap/ee-supported-rhel8-vault:${TAG}
podman push --tls-verify=false ${HOST}/aap/ee-supported-rhel8-vault:${TAG}
```
