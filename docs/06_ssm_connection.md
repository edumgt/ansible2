# AWS SSM Session Manager로 SSH 없이 Ansible 운영

## 개념
- 일반적으로 Ansible은 SSH로 접속하지만, AWS에서는 **SSM(Session Manager)**를 이용해
  - **22 포트를 열지 않고도**
  - **VPC 내부 프라이빗 인스턴스에도**
  - AWS IAM 권한으로 안전하게 접속할 수 있습니다.

## 준비물
1) 대상 EC2에 **SSM Agent**가 설치/실행 (Ubuntu/Amazon Linux는 기본 포함인 경우 많음)
2) EC2 인스턴스 프로파일(역할)에 권한 부여
   - 예: `AmazonSSMManagedInstanceCore`
3) 운영 PC에
   - AWS CLI
   - session-manager-plugin

## Ansible에서 SSM 연결 사용
이 레포는 `amazon.aws` 컬렉션의 **aws_ssm 연결 플러그인**을 가정합니다.

예시(host_vars 또는 group_vars로 지정):

```yaml
ansible_connection: amazon.aws.aws_ssm
ansible_aws_ssm_region: ap-northeast-2
ansible_user: ubuntu
```

> 참고: SSM은 SSH 키가 필요 없지만, IAM 권한/인스턴스 역할이 정확히 설정되어야 합니다.

## 트러블슈팅 체크리스트
- EC2의 SSM 관리형 인스턴스로 등록되었는지(AWS 콘솔 Systems Manager)
- 인스턴스가 인터넷/프라이빗 SSM 엔드포인트를 통해 SSM에 통신 가능한지
- IAM 사용자/역할 권한에 `ssm:StartSession` 등이 포함되는지
