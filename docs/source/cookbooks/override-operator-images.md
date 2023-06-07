# Override operator images

Since the Framework relies on [install_yamls](https://github.com/openstack-k8s-operator/install_yamls),
you have to leverage the Makefile environment variables in order to override
operator images.

In order to do so, you have to:
- get a hold on the correct parameter for the operator(s) you want to override.
- inject a custom environment file in the ci-framework run.

Let's say, you want to override `mariadb` operator:
- Get the parameter(s) from the [Makefile](https://github.com/openstack-k8s-operators/install_yamls/blob/main/Makefile)
you'll see `MARIADB_IMG`. That's your parameter
- create an environment file with this content:
```YAML
---
cifmw_install_yamls_vars:
  MARIADB_IMG: https://your.registry.tld:5001/my-mariadb-image:latest
```

Just provide that file to `ansible-playbook`:
```Bash
$ ansible-playbook deploy-edpm.yml -e @my-env.yml [-e @some/other/env ...]
```
and you're set!
