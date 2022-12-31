# 개요
* kubernetes headless 서비스 테스트

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

# 삭제 방법
```sh
kubectl delete -k ./
```
