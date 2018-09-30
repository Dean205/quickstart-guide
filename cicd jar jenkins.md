- ### ����jenkins
1. ����Amazon EC2ʵ����ѡ��ʵ�����ͺ���Ӵ洢��
   ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-1.png)
2. �ڡ��߼���ϸ��Ϣ���������������ű�
   ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-2.png)

```
#!/bin/bash
yum -y update
yum install -y ruby
yum install -y aws-cli
yum install �Cy git
cd /home/ec2-user
wget https://bucket-name.s3.amazonaws.com/latest/install
chmod +x ./install
./install auto

```
3. bucket name��Ӧ�б�Ϊ
    ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-3.png)
4.  EC2�����ɹ���ʹ��SSH����EC2��ʹ�������������Agent�Ƿ���������

```
sudo service codedeploy-agent status
Result: The AWS CodeDeploy agent is running as PID 3523

```
- ### ʹ��Github�й�Դ���룬������webhook�Զ�����
1. ���Ƚ����Լ���Github��ַ�����https://github.com/settings/tokens������GitHub token�����token����jenkins����GitHub��

    ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-4.png)
2. Ϊ��Ҫ��CI/CD��GitHub����hook��ʵ�ִ�������Զ�֪ͨJenkins��Payload URL����Jenkins Server�ĵ�ַ��Ĭ��Jenkins����8080�˿ڡ���¼�����ɵ�token�ַ��������磺 bf6adc27311a39ad0b5c9a63xxxxxxxxxxxxxx
3. ����һ���µ�repository
   ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-5.png)
4. �������λ�������Ҫ��Git�ֿ⣬������ΪAWS-BJS-CodeDeploy-CICD-Jenkins�������Settings������webhooks��
   ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-6.png)
5. �����Add Webhooks��
6. ��Payload URL������http://EC2����IP��ַ/github-wekhook/������ͼ��ʾ��
    ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-7.png)
- ### ����Jenkins������װCodeDeploy���
1. ��װ��νű���װJenkins��Ĭ��Java�Ļ�����1.7�ģ�������������Java 1.8�汾��

```
sudo -s
java �Cversion
yum install java-1.8.0
yum remove java-1.7.0-openjdk
wget -O /etc/yum.repos.d/jenkins.repo http://jenkins-ci.org/redhat/jenkins.repo
rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
yum install jenkins
chkconfig jenkins on
service jenkins start
//�鿴JenkinsĬ������
cat /var/lib/jenkins/secrets/initialAdminPassword

```
2. ���������������EC2�Ĺ���IP��ַ����ð�һ������EIP��������54.223.215.xx:8080��Ȼ��������½��棬��������õ���Ĭ�����롣
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-8.png)
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-9.png)
3. �����û��������룬�͵����½��棬���ʱ��Jenkins�Ϳ��Խ��������ˡ�
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-10.png)
4. ����ϵͳ����
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-11.png)
5. ����Jenkins URL�������Add�����Jenkins
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-12.png)
6. ����Github��ȡ��Access Token���������ӡ���
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-13.png)
7. �����Test Connection����û�б���˵�����óɹ���
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-14.png)
8. ��ӹ�����
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-15.png)
9. ���AWS CodeDeploy�Ĳ���������Install without restart��
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-16.png)
10. �½�һJenkins����Ŀ�������Create a new project��
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-17.png)
11. ����Github��Ŀ�ĵ�ַ��Դ�������ѡ��Git��ʽ��
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-18.png)
12. ����������ѡ��Github hook trigger for GITScm polling
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-19.png)
13. ѡ����ӹ������衱
    ѡ��AWS cloud build�����
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-20.png)
14. ���ౣ�ֿհ�
    �������ӹ������衱
    ѡ��ִ�� shell
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-21.png)
15. 
```
aws s3 cp s3://yuan0928/target/test_springboot.jar ./   //����codeBuild��д���ļ������λ��
mkdir target
mv test_springboot.jar target/

```

   �����нű�����˼�ǰ���һ�������ɵ�jar����ӵ������У���������Ĳ�������
16. ѡ��Post-build Actions��������CodeDeploy�����Ϣ������ѡ�������ڵ�code deploy��region
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-22.png)
17. ��֤��ʽ��������AWS Access Key��Security Key�������������������ʹ����ʱ��credentials��
     ![ͼƬ1](./assets/cicd-jar-jenkins/cicd-jar-jenkins-23.png)
18. �����Ӧ�á� �����桱