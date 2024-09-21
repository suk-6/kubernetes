# Kubernetes Settings

## General

쿠버네티스 설치하기

```bash
sudo sh kubernetes.sh
```

## master

`kubernetes.yaml`에서 `controlPlaneEndpoint`와 `certSANs`를 Master Node의 Private IP로 변경

```bash
sudo kubeadm init --config kubernetes.yaml
```

생성하고 나오는 Join 명령어 복사

### Azure Settings

`/etc/kubernetes/azure.json`에 `azure.json` 파일 채워서 넣기

```bash
sudo sh helm.sh

helm install --repo https://raw.githubusercontent.com/kubernetes-sigs/cloud-provider-azure/master/helm/repo cloud-provider-azure --generate-name --set cloudControllerManager.imageRepository=mcr.microsoft.com/oss/kubernetes --set cloudControllerManager.imageName=azure-cloud-controller-manager --set cloudNodeManager.imageRepository=mcr.microsoft.com/oss/kubernetes --set cloudNodeManager.imageName=azure-cloud-node-manager
```

## worker

`kubejoin.yaml`에서 `bootstrapToken`을 Master에서 생성한 Token으로 변경

```bash
sudo kubeadm join --config kubejoin.yaml
```

## Shell

```bash
kubectl run -it --rm --restart=Never busybox --image=gcr.io/google-containers/busybox sh
```
