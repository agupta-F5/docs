```

$vim ~/.bashrc


alias ocdebugedit='oc edit deploy/k8s-bigip-ctlr-deployment -n kube-system'
alias ocdebuglog='oc logs deploy/k8s-bigip-ctlr-deployment -n kube-system -f'
alias ocdebugscale0='oc scale deployment/k8s-bigip-ctlr-deployment -n kube-system --replicas=0'
alias ocdebugscale1='oc scale deployment/k8s-bigip-ctlr-deployment -n kube-system --replicas=1'
alias occtrl='oc get deploy -n kube-system'

alias ocedit='oc edit deploy/test-bigip-controller-1 -n kube-system'
alias oclog='oc logs deploy/test-bigip-controller-1 -n kube-system -f'
alias ocscale0='oc scale deployment/test-bigip-controller-1 -n kube-system --replicas=0'
alias ocscale1='oc scale deployment/test-bigip-controller-1 -n kube-system --replicas=1'


$source ~/.bashrc

$ unalias alias_name
$ unalias -a [remove all alias]
```