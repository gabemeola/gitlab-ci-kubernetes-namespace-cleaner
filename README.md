# Gitlab CI Kubernetes namespace cleaner

If you are using Gitlab to automatically deploy to Kubernetes using Gitlab CI and Gitlab environments, you might have noticed that when environments (deployments) are removed, the `Namespace` resource will stay around forever. Gitlab simply does not remove it (yet). There is an official issue for this that you can find [here](https://gitlab.com/gitlab-org/gitlab/issues/27501). Until the issue is resolved, this cleaning tool might help you out! It's a simple tool, written in Golang, that can be deployed to your cluster as a `CronJob` that removes these stale namespaces on a daily basis.

**Note:** This will check all namespaces that matches the pattern `^gitlab-ci-test-.+` and has no running pods and **delete** them. If you have namespaces that matches this pattern that does not run any pods and you want to keep them, **do not run this tool**.


## Building

```shell
$ make
```


## Running outside cluster

```shell
$ bin/gitlab-ci-kubernetes-namespace-cleaner-linux-amd64 clean --kubeconfig /home/myuser/.kube/config
```