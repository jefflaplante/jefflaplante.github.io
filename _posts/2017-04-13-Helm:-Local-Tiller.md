Helm is an awesome package management tool for Kubernetes. I highly recommend it. It comes in two go binaries - helm, the cli we work with and tiller - the server component that does most of the real work.

Normally Tiller is installed as a deployment on the Kubernetes cluster you wish to work with. However, this poses a security risk in that Tiller is not secured out of the box. As such, do NOT run the default `helm init`.

Happily, you do not need to install Tiller on the Kubernetes cluster to work with it. You can and should run the tiller binary locally on the bastion host. Tiller and Helm use your kubectl configs to determine what Kubernetes cluster to interact with.

```
tiller &
Tiller is listening on :44134
Probes server is listening on :44135
Storage driver is ConfigMap
```

You also have to tell helm that it should look locally to find tiller:
```
export HELM_HOST=localhost:44134
```

Once tiller is running you can run helm commands are you would if tiller were installed on your Kubernetes cluster.
```
helm version
Client: &version.Version{SemVer:"v2.1.0", GitCommit:"7389b341c767259a8367132b72035e59a5ee67c7", GitTreeState:"clean"}
Server: &version.Version{SemVer:"v2.1.0", GitCommit:"7389b341c767259a8367132b72035e59a5ee67c7", GitTreeState:"clean"}
```
