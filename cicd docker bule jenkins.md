##### 1. �������ɷ�����Ŀ
##### 2. ����github��Ŀ�ĵ�ַ
  ![ͼƬ1](./assets/cicd-docker-jenkins/cicd-docker-jenkins-1.png)
##### 3. ����github��Ŀ��git��ַ�ͷ�֧
  ![ͼƬ1](./assets/cicd-docker-jenkins/cicd-docker-jenkins-2.png)
##### 4. ��ѡGithub hook trigger for GITScm polling  ʵ��github������µ��Զ�����
  ![ͼƬ1](./assets/cicd-docker-jenkins/cicd-docker-jenkins-3.png)
##### 5. �������ӹ������衱  ѡ��AWS cloud build�����
##### 6. ����aws��accessId ��accessKey
##### 7. ����code build��Ŀ����Ŀ���ƺͿ�����
  ![ͼƬ1](./assets/cicd-docker-jenkins/cicd-docker-jenkins-4.png)
##### 8. �������ӹ������衱  ѡ��AWS cloud build�����
##### 9. ����aws��accessId ��accessKey
##### 10. ����code build��Ŀ����Ŀ���ƺͿ�����
##### 11. ����ĿĿ��Ϊ��Դ����Ϊjar�����ϴ���S3Ͱ��
  ![ͼƬ1](./assets/cicd-docker-jenkins/cicd-docker-jenkins-5.png)
##### 12. ѡ����ӹ������衰
##### 13. ѡ��ִ�� shell��
  ![ͼƬ1](./assets/cicd-docker-jenkins/cicd-docker-jenkins-6.png)
  
  ���δ�����߼��ǣ�
1.	����build_numberҲ����ÿ��build�Ļ�������ֵ�������ж�ʹ���ĸ�������ģ��  �������ڲ�ͬ��ģ����������ʵ���Ķ˿ںŶ�Ӧ��ͬ
2.	�����µĲ��������µ������壬
3.	���·��������е�����Ϊ������

##### 14. �������ӹ����������
##### 15.ѡ�� lambda invocation
1. ��дacces Id��access Key
2. ��дlambda���ڵĿ������ͼ������õ�lambda����
  ![ͼƬ1](./assets/cicd-docker-jenkins/cicd-docker-jenkins-7.png)

Lambda�߼�Ϊ��

1. Elb��������������  80 8080 1234 �ֱ��Ӧ����Ŀ���� tg1 tg2
2. Ŀ������һ��tag: isProduction:Boolean  �����Ŀ����Ŀǰ�ǲ���������������Ŀ����
3. ���ǽ����¹��ķ�����������Ŀ���� ��Ϊ80�˿ڵļ���Ŀ����  ���з������
���Ҹ���Ŀ�����tag

##### 16. �����Ӧ�á������桰
##### 17. ���������������
