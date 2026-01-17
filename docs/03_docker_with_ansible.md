# Docker 운영 자동화

## 목표
- 서버 OS에 맞게 Docker 엔진을 설치/업데이트
- Compose 프로젝트를 배포
- 헬스체크로 정상 상태 확인

## 실행
```bash
ansible-playbook -i inventories/dev/hosts.ini playbooks/10_docker_engine_install.yml
ansible-playbook -i inventories/dev/hosts.ini playbooks/11_deploy_stack.yml
```
