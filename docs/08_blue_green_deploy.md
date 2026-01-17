# Blue-Green 배포(단일 호스트)

## 아이디어
- 같은 서버에 `blue` / `green` 두 개의 스택을 올려두고
- 현재 서비스 중인(active) 스택은 유지
- inactive 스택에 새 버전을 배포 → 헬스체크 통과 → nginx 업스트림을 교체 → reload

## 실행
```bash
ansible-playbook -i inventories/dev/hosts.ini playbooks/13_blue_green_switch.yml
```

## 장점/주의
- 장점: 롤백 쉬움(업스트림 다시 스위치)
- 주의: 한 서버에서 리소스를 2배로 사용할 수 있음
