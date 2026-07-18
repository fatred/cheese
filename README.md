# cheese
---

A simple example deployment for k8s. 

Pre-req: Install the carver tools 

---

ytt only: 

1. customise the cheese.defaults.yaml as you see fit.
2. render and check it on screen

```shell
ytt -f .
```

3. render again and push direct to the cluster

```shell
ytt -f .  | kubectl apply -f -
```

---

kapp + ytt

1. customise the cheese.defaults.yaml as you see fit.
2. check the includes in the ytt are "complete" and then run a deploy

```shell
kapp deploy -a cheese -f <(ytt -f .)
```
