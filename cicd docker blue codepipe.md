- ### ����codebuild��Ŀ
1. ����Ŀ������Ŀ��Ϊ��java��������jar��
2. ������Ŀ���ƺ�Դ��洢�ĵط�  ��github  github��Ŀurl
  ![ͼƬ1](./assets/cicd-docker-codepipe/cicd-docker-codepipe-1.png)
3. ѡ��ubuntuΪ��������
4. ѡ��Java������openjdk-java9�İ汾
5. ѡ��buildspex.yml����Ϊ�����ű�
  ![ͼƬ1](./assets/cicd-docker-codepipe/cicd-docker-codepipe-2.png)
6. ѡ��S3��Ϊ���������
7. ������Ϊ�����S3Ͱ������
  ![ͼƬ1](./assets/cicd-docker-codepipe/cicd-docker-codepipe-3.png)
8. ѡ��codebuild��ִ�н�ɫ
  ![ͼƬ1](./assets/cicd-docker-codepipe/cicd-docker-codepipe-4.png)
- ###  �����µ�codeBuild��Ŀ  
1. ����Ŀ��Ŀ��Ϊ��jar������Ϊdockers����
2. ������Ŀ���ƺ�Դ��洢�ĵط�  ��github  github��Ŀurl
  ![ͼƬ1](./assets/cicd-docker-codepipe/cicd-docker-codepipe-5.png)
3. ѡ��ubuntuΪ����ϵͳ
4. ����Ϊdockers
5. ���а汾Ϊaws codebuild docker
  ![ͼƬ1](./assets/cicd-docker-codepipe/cicd-docker-codepipe-6.png)
6.���빹������

```
version: 0.2
phases:
  pre_build:
    commands:
      - $(aws ecr get-login --no-include-email)
      - TAG=v_${BUILD_NUMBER}
      - echo $TAG
      - aws s3 cp s3://<���������s3Ͱ��ַ> /test_springboot.jar ./
  build:
    commands:
      - docker build -t 859407660328.dkr.ecr.us-east-1.amazonaws.com/codevpcregis:$TAG .
  post_build:
    commands:
      - docker push "859407660328.dkr.ecr.us-east-1.amazonaws.com/codevpcregis:$TAG"
      - printf '{"tag":"%s"}' $TAG > build.json
artifacts:
  files: build.json

```
7. ѡ���޹���   �޻���
  ![ͼƬ1](./assets/cicd-docker-codepipe/cicd-docker-codepipe-7.png)
8.ѡ��codeBuild�Ľ�ɫ
  ![ͼƬ1](./assets/cicd-docker-codepipe/cicd-docker-codepipe-8.png)
9. �������