# cheese
---

A simple example deployment for k8s. 

Pre-req: Install the carvel tools (https://carvel.dev/ytt/docs/v0.52.x/install/) or just `wget -O- https://carvel.dev/install.sh | sudo bash -`

check your defaults match. specifically, pick the right gateway class for your env (default is `cloud-provider-kind`, you might like to have `cilium`)

read more about ytt here: https://carvel.dev/ytt/
read more about kapp here: https://carvel.dev/kapp/ 
read more about the cloud-provider-kind here: https://github.com/kubernetes-sigs/cloud-provider-kind?tab=readme-ov-file

use helm instead of ytt in front of kapp: `kapp -y deploy -a my-chart -f <(helm template my-chart --values my-vals.yml)`

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

---

get the IP that the cloud-provider used for your gateway instance
`kubectl get gateway -n cheese`
```
NAME     CLASS                 ADDRESS      PROGRAMMED   AGE
cheese   cloud-provider-kind   172.19.0.3   True         46m
```

_If you need to, use `ssh -D 1080 jump` to be able to get to this IP via a SOCKS5 proxy in your second browser_

you can then test with a web browser to see the cheese.

based on the above IP:
http://172.19.0.3/cheddar: ![cheddar](./images/cheddar.png)

http://172.19.0.3/stilton:
![stilton](images/stilton.png)

http://172.19.0.3/wensleydale:
![wensleydale](images/wensleydale.png)
