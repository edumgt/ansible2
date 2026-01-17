# Rolling 배포(멀티 호스트)

## 아이디어
- 서버가 여러 대일 때, **한 대씩** 업데이트하고 헬스체크를 통과하면 다음 서버로 넘어갑니다.
- Ansible에서는 `serial: 1` 로 쉽게 구현합니다.

## 실행
```bash
ansible-playbook -i inventories/prod/hosts.ini playbooks/12_deploy_stack_rolling.yml
```

## 장점/주의
- 장점: 장애 범위 최소화
- 주의: 외부 로드밸런서/트래픽 제어가 있으면 더 안정적(드레인/가중치)
