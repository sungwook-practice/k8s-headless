# 개요
* kubernetes headless 서비스 테스트
* 유투브 영상: https://youtu.be/If03sN4isO4

# 실행방법
* steatefulset storageClassName 수정
```yaml
vi ./headless-service/statefulset.yaml

...
volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: ["ReadWriteOnce"]
      storageClassName: openebs-hostpath
      ...
```

* 배포
```sh
kubectl apply -k ./
```

# 로드밸런싱 테스트
* normal
```sh
for i in $(seq 1 10);do curl -s echo-normal.default.svc | jq ".environment.HOSTNAME";done | sort -n | uniq -c
```

* headless
```sh
for i in $(seq 1 10);do curl -s echo-headless.default.svc | jq ".environment.HOSTNAME";done | sort -n | uniq -c
```

# A record 확인
* normal
```sh
nslookup -type=srv echo-normal.default.svc
```

* headless
```sh
nslookup -type=srv echo-headless.default.svc
```

# 삭제 방법
```sh
kubectl delete -k ./
```
