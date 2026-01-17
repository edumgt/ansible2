# AWS 원샷 구성(프로비저닝 → SSM → 배포)

## 구성 흐름
1) VPC/서브넷/IGW/라우팅/SG 생성
2) SSM용 IAM Role + Instance Profile 생성
3) EC2 생성(SSH 포트 미오픈) + 태그(AnsibleManaged=true)
4) 동적 인벤토리로 EC2 자동 검색
5) SSM 연결로 Docker/Compose 배포

## 실행
```bash
ansible-playbook playbooks/20_aws_provision_ssm_no_ssh.yml -e aws_region=ap-northeast-2 -e environment=dev
ansible-inventory -i inventories/aws/aws_ec2.yml --graph
ansible-playbook -i inventories/aws/aws_ec2.yml playbooks/21_post_provision_via_ssm.yml
```

정리:
```bash
ansible-playbook playbooks/23_aws_cleanup.yml -e aws_region=ap-northeast-2 -e environment=dev
```
