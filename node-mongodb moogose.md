##node

###nodeָ��
	node 	      --�������̨		
	node -v 	  --�鿴�汾
	node filename --�����ļ�	

�������
	���ݿ������>>>���ݿ�>>>����>>>�ĵ�
	*�����кܶ����ݿ�>�����ж������>�����ж���ĵ�(��С��λ,��������Ķ���)
##1.mongo ����mongodb,�����ͻ���

##2.mongod ��������������
1.��װMongoDB
	- ��װ
	- ���û�������
		C:\Program Files\MongoDB\Server\3.2\bin
	- ��c�̸�Ŀ¼
		- ����һ���ļ��� data
		- ��data�д���һ���ļ���db
		
	- ��cmd�����д���
		- ���� mongod ����mongodb������
		- 32λע�⣺
			����������ʱ����Ҫ������������
				mongod --storageEngine=mmapv1
				
				mongod --dbpath ���ݿ�·�� --port �˿ں�


		
	- �ڴ�һ��cmd����
		- ���� mongo ����mongodb ������ > 
		
	- ���ݿ⣨database��
		- ���ݿ�ķ�����
			- ������������������
			- mongod ��������������
			
		- ���ݿ�Ŀͻ���
			- �ͻ������������������������ݽ�����ɾ�Ĳ�Ĳ���
			- mongo ���������ͻ���
			
			
	- ��MongoDB����Ϊϵͳ���񣬿����Զ��ں�̨����������Ҫÿ�ζ��ֶ�����
		1.��c�̸�Ŀ¼����data
			- ��data�´���db��log�ļ���
		2.���������ļ�
			��Ŀ¼ C:\Program Files\MongoDB\Server\3.2 �����һ�������ļ�
			mongod.cfg
		3.�Թ���Ա����ݴ������д���	
		
		4.ִ�����µ�����
			sc.exe create MongoDB binPath= "\"C:\Program Files\MongoDB\Server\3.2\bin\mongod.exe\" --service --config=\"C:\Program Files\MongoDB\Server\3.2\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"
			
			sc.exe create MongoDB binPath= "\"mongod��binĿ¼\mongod.exe\" --service --config=\"mongo�İ�װĿ¼\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"
			
		5.����mongodb����

		6.�������ʧ�ܣ�֤���ϱߵĲ�������
			�ڿ���̨���� sc delete MongoDB ɾ��֮ǰ���õķ���
			Ȼ��ӵ�һ������һ��


	- ��������
		���ݿ⣨database��
		���ϣ�collection��
		�ĵ���document��
			- ��MongoDB�У����ݿ�ͼ��϶�����Ҫ�ֶ�������
				�����Ǵ����ĵ�ʱ������ĵ����ڵļ��ϻ����ݿⲻ���ڻ��Զ��������ݿ�ͼ���
		
	- ����ָ��
		show dbs
		show databases
			- ��ʾ��ǰ���������ݿ�
		use ���ݿ���
			- ���뵽ָ�������ݿ���
		db
			- db��ʾ���ǵ�ǰ���������ݿ�
		show collections
			- ��ʾ���ݿ������еļ���
			
	- ���ݿ��CRUD����ɾ�Ĳ飩�Ĳ���
		- �����ݿ��в����ĵ�
			db.<collection>.insert(doc)
				- �򼯺��в���һ���ĵ�
				- ���ӣ���test���ݿ��еģ�stus�����в���һ���µ�ѧ������
					{name:"�����",age:18,gender:"��"}
					db.stus.insert({name:"�����",age:18,gender:"��"})
			
			db.<collection>.find()
				- ��ѯ��ǰ�����е����е��ĵ�

- �����ݿ��в����ĵ�
			- db.collection.insert()
				- insert()�����򼯺��в���һ�������ĵ�
			- db.collection.insertOne()
				- �򼯺��в���һ���ĵ�
			- db.collection.insertMany()
				- �򼯺��в������ĵ�
				
		- ��ѯ���ݿ��е��ĵ�
			- db.collection.find()
				- ���Ը���ָ�������Ӽ����в�ѯ���з����������ĵ�
				- ���ص���һ������
			- db.collection.findOne()
				- ��ѯ��һ�������������ĵ�
				- ���ص���һ������
			- db.collection.find().count()
				- ��ѯ�����������ĵ�������
				
		- �޸����ݿ��е��ĵ�
			- db.collection.update()
				- �����޸ġ��滻�����е�һ�������ĵ�
			- db.collection.updateOne()
				- �޸ļ����е�һ���ĵ�
			- db.collection.updateMany()
				- �޸ļ����еĶ���ĵ�
			- db.collection.replaceOne()
				- �滻�����е�һ���ĵ�
				
		- ɾ�������е��ĵ�
			- db.collection.remove()
				- ɾ�������е�һ�������ĵ���Ĭ��ɾ�������
			- db.collection.deleteOne()
				- ɾ�������е�һ���ĵ�
			- db.collection.deleteMany()
				- ɾ�������еĶ���ĵ�
			- ���һ������
				db.collection.remove({})
			- ɾ��һ������
				db.collection.drop()
			- ɾ��һ�����ݿ�
				db.dropDatabase()



db.<collection>.insert(doc) - �����ݿ��в����ĵ�

db.<collection>.find()      - ��ѯ��ǰ�����е����е��ĵ�

objectId()                  - ����id,����ʱ������(id��ȷ����ϢΨһ��)�����Լ�ָ��,����Ҳ����ȷ��Ψһ��;

###mongodb--IDE(mongodbmanagerfree_inst)
F6 ִ�й�������еĴ���
F9 ִ��ѡ�ж���

##mongoose
	/*
  1. ����mongooseģ��
  2. ���ӱ���mongoDB���ݿ�
  3. ����Schemaģʽ����
  4. ����Modelģ�Ͷ���
  5. ����Document�ĵ�����
  6. ��������
 */
 
 /*
      ģ�Ͷ����CRUD
      C - create
        Model.create(�ĵ�����, �ص�����)  ����ֵΪundefined
        Model.create(�ĵ�����)  ����ֵΪpromise
      R - read
        Model.find(��ѯ����[, ͶӰ], �ص�����)
        Model.find(��ѯ����[, ͶӰ])
        Model.findOne(��ѯ����[, ͶӰ])
        
        ��������
          1. < <= > >= !==  $lt $lte $gt $gte $ne
          2. ��� $or $in �� $nin
        
      U - update
        Model.updateOne(��ѯ����, ���µ�����[, ���ö���])
        Model.updateMany(��ѯ����, ���µ�����[, ���ö���])
      D - delete
        Model.deleteOne(��ѯ����)
        Model.deleteMany(��ѯ����)
     */
	 
	 ����CRUD�ķ���ֵ��Promise��װ����
	 
	 ��������async await����  �ȵ���Ҫ�ķ���ֵ