# egis-converter-vector-manifest

`egis-converter-vector`(벡터 변환 서비스)의 쿠버네티스 배포 설정을 관리하는 CI/CD용 저장소입니다.

---

## 파일 구성

| 파일                        | 설명                                            |
| --------------------------- | ----------------------------------------------- |
| `egis-consumer-vector.yaml` | 배포 설정 (Deployment, HorizontalPodAutoscaler) |

---

## 배포 설정 요약

### 자동 확장 (HPA)

| 항목         | 값                  |
| ------------ | ------------------- |
| 최소 파드 수 | 1                   |
| 최대 파드 수 | 3                   |
| 확장 기준    | 평균 CPU 사용률 70% |

### 종료 처리

파드가 종료될 때(`preStop`) 5분 평균 부하(load average)가 0.5 이하로 내려갈 때까지 5초 간격으로 확인하며 기다린 뒤 종료합니다.
종료 유예 시간(`terminationGracePeriodSeconds`)이 30초이므로, 30초가 지나면 부하와 관계없이 종료됩니다.
