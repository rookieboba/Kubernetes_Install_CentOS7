[환경]
CentOS7

[서버 구성]
- master 서버 3대
  - master1 / master2 / master3
- worker 서버 2대
  - worker1 / worker2
- lb 서버 1대
  - lb
  
준비 후 아래 과정 진행

[모든 서버] 
1. /etc/hosts 설정 필수
  - 위의 6대가 전부 등록되어 있어야 한다

```
예시)
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

192.168.98.149 master1
192.168.98.150 master2
192.168.98.151 master3
192.168.98.152 worker1
192.168.98.153 worker2
192.168.98.154 lb
```

2. Kubernetes Install 적용
 
[lb 서버]

3. multi-master 단일 진입점인 LoadBalancer 구성 (LB)
   - server ip 설정 주의 

[master 서버]

4. kubeadm 이용 HA 클러스터 구성
etcd 가 동기화 되게 하기 위한 작업

4-1 ) [master1]
```
kubeadm init --control-plane-endpoint "{로드벨런서 서버 hostname}:6443" --upload-certs
예시) kubeadm init --control-plane-endpoint "lb:6443" --upload-certs
```
결과로 출력되는 kubeadm join 명령어 줄 복사하기
그 후, 다른 master 서버에서 붙여넣기 

4-2) [master2]

4-3) [master3]
