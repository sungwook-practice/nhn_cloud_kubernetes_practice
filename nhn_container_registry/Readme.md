# 개요
* NKS에서 NCR사용 예제

# 전제조건
* NCR 생성

# pod 생성방법
* secret 생성
```shell
kubectl create secret docker-registry registry-credential \
  --docker-server={사용자 레지스트리 주소} \
  --docker-username={NHN Cloud 계정 email 주소} \
  --docker-password={서비스 Appkey 또는 통합 Appkey}
```

## 컨테이너 이미지 push
* 예제에서는 dockerhub를 사용
```shell
# dockerhub에 있는 nginx컨테이너이미지 pull
docker pull nginx:1.24.0

# registry 컨테이너 이미지 생성
docker tag nginx:1.24.0 {사용자 레지스트리 주소}/nginx:1.24.0

# 컨테이너 이미지를 NCR에 push
docker push {사용자 레지스트리 주소}/nginx:1.24.0
```

## pod 생성
* pod.yaml에서 registry주소와 컨테이너 이미지를 수정

* pod 생성
```shell
kubectl apply -f pod.yaml
```

# 예제 삭제
```shell
kubectl delete -f pod.yaml
kubectl delete secret registry-credential
```