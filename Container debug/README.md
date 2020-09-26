# How to set it up

### Creating debug image
```
$make debug
```
Docker tag it
Docker push
##### Note: debug image cannot be run with regular deployment, so better to choose a different naming patter for debug images, such as extending the name with "_dbg", etc

#### Deploy CIS debug container in the ecosystem (K8S/OpenShift)

```
oc create -f cis_debug_deploy.yaml
```

Expose the deployment with a service in node port mode, so that the container would be reachable from outside the cluster
```
oc create -f cis_debug_svc.yaml
```
Create an ssh tunnel to the container from the local machine through bastion
For this the below info is required
Ip of any node from the cluster
```
oc get nodes -o wide
```
Take INTERNAL-IP of any node 
node port that was exposed by the debug service created
```
oc -n kube-system get svc cis-dbg-svc
```
Take PORT
Ability to login to bastion of the setup
```
ssh -L <localport>: <node_ip>:<node_port> root@bastion
ssh -L 40000:172.16.1.116:31620 root@10.145.74.218
```
Configure remote debug in the IDE
* GoLand
TooBar: Run >> Edit Configurations
Add a profile
Host: localhost (or) 127.0.0.1
Port: 40000
* VsCode
Select the Run icon in the Activity Bar on the side of VS Code.
Add Configureation
```
{
    "version": "0.2.0",
    "configurations": [
        {
        "name": "Connect to server",
        "type": "go",
        "request": "attach",
        "mode": "remote",
        "port": 40000,
        "host": "127.0.0.1",
        "trace": "log",
        "showLog": true,
        "cwd": "${workspaceRoot}",
        "logOutput": "rpc"
    }
    ]
}
```
Start debugging by starting the debugger in the IDE.