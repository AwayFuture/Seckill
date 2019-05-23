
							> > > �߲�����ɱϵͳ < < <
					 
	1. ʹ�õĿ�ܣ�SpringMVC + Spring + MyBatis	+ JSP + Bootstrap + JQuery
	
	2. ϵͳ��ܵļ�����
		(1)MySQL�㣺����ơ�SQL������������м���
		(2)MyBatis�㣺DAO�����ơ�MyBatis����ʹ�á�MyBatis��Spring������
		(3)Spring�㣺SpringIOC����Service������ʽ���������
		(4)SpringMVC�㣺Restful�ӿڵ������ʹ�á�����������̡�Controller��������
		(5)ǰ�ˣ�������ơ�Bootstrap��jQuery
		(6)�߲������߲�����͸߲����������Ż�˼·��ʵ��
		
	3. maven��Ŀ�Ĵ:
		mvn archetype:generate 
		-DgroupId=com.gdufe.seckill -DartifactId=seckill
		-DarchetypeArtifactId=maven-archetype-webapp
		-DinteractiveMode=false
	
	4. ����Ŀ���뵽IntelliJ IDEA�У�����
	   (1) �޸�web.xml��servlet�汾Ϊ���µİ汾[�ӹ�����ȡ���ߴӰ���servlet��Ŀ�л�ȡ]
	   (2) ��ȫmaven��Ŀ��Ŀ¼�Ǽ�[Project Structure����Ŀ¼�ļ���]
	   (3) ��pom.xml�������Ŀ�������������[Get From MVN-Website]
					
	5. ��ɱҵ����ѵ�: �߲����µ�Ч������ + ���� + �м���
	
	6. ��Ҫ˼�������⣺������ܵľ���ʹ�ó����͹���
	
				
һ��Java�߲�����ɱAPI֮DAO��
	
	1. ���ݿ������[SQL��д(engine=InnoDB + auto_increment=1000 + comment)]
	
	2. Dao�ӿڵ����: �������ݿ�����ӳ���ϵ�Ľӿڷ������(@Param����������)
	
	3. MyBatis��mapper.xml�ļ���SQL��д
		>> #{seckillId}��<![CDATA[<=]]>
		>> resultType��parameterType��statementType
		>> limit��ignore��as��[table1] inner join [table2] on [��������]
		>> call �洢����: #{seckillId,jdbcType=BIGINT,mode=IN}

	4. mybatis-config.xml��������mybatis��ȫ�����ã����շ�����ת����
						<setting name="mapUnderscoreToCamelCase" value="true"/>
		
	5. Spring-MyBatis��������
		>> ����dataSource -> com.mchange.v2.c3p0.ComboPooledDataSource
		>> ����sqlSessionFactory -> org.mybatis.spring.SqlSessionFactoryBean
		>> ����spring-mybatisӳ��Ľӿ�ʵ�����Mapper -> 
							org.mybatis.spring.mapper.MapperScannerConfigurer
							(ע������springɨ��Ľӿڰ���location : basePackage)
	
	6. myBatis����Spring��ܣ�Ҫ��+�ѵ㣩
	   1.���߲��Գ��ֵ�BUG������취��
		(1) ��xxxDao.xml�ӿ���(Ctl+Shift+T) Create Testʱû���ҵ���ѡ��ķ�����
			�� ���ӿ�interface��ʱ��Ϊclass����ʹ��ͬ���ķ���ȥ���Ϳ����ˣ�Ȼ���interface�Ļ���
			�� ���õ���2019�°汾��IDEA����˵�ǰ汾������
			
		(2) mapUnderscoreToCamelCase ������ mapUnderscoreCamelCase
		
		(3) ���ݿ�����ʧ�ܣ�Access denied for user "LU131@localhost" ...
			�� ������ݿ��������? Driver + url + username + password �Ƿ���ȷ
			�� �ҵ�Error--> url=jdbc:mysql://localhost:3306/seckill?useUnicode=true&characterEncoding=utf8
			  �޸�urlΪ��url=jdbc:mysql://localhost:3306/seckill?serverTimezone=GMT%2B8 ���ӳɹ�
			�� ��õ�url:url=jdbc:mysql://localhost:3306/seckill?useUnicode=true&characterEncoding=utf8&serverTimezone=GMT%2B8
			  
		(4) at com.mchange.v2.c3p0.impl.NewProxyResultSet.isClosed?
			�� ���ָ�BUG��ԭ����c3p0��JDBC��֧����ԭ�򣬽�pom.xml��c3p0�汾��Ϊ0.9.2.x���ϵİ汾���ɽ��������
			�� �ο�GitHub����������https://github.com/swaldman/c3p0/issues/18
			

����Java�߲�����ɱAPI֮Service��	
	
	1. Java�е��쳣: �������쳣 + �������쳣
		>> �����ڵ��쳣����Ҫ�ֶ�ȥtry+catch
		   �ο�: https://blog.csdn.net/yuming226/article/details/83313273
	    >> Spring����ʽ����ֻ���ܳ����������쳣�ع�����
	
	2. ΪʲôҪʹ��Spring IOC (Ҳ��Ϊ����ע��DI)?
		(1) ���󴴽�ͳһ�йܣ��������ڳ�����ͨ��new�ķ�ʽȥ����
		(2) �淶���������ڹ�������init()��destroy()
		(3) ��������ע��
		(4) һ�µĻ�ȡ���󣬿�����IOC�����л�ȡ��Ҫ������ʵ��������Щ����ʵ��
			Ĭ�϶���singleton(����ģʽ)
			
	3. Spring�еĸ��ֳ���ע�����:https://www.cnblogs.com/xiaoxi/p/5935009.html
	
		>> resources�ļ����µ�spring-xxx.xml��ɨ�赽��packageֻ��src/mainĿ¼��,
		  testĿ¼�Ĳ���packageɨ�費��,��test�ļ����µ�classʹ��@Serviceע����
		  Ч��,���ǲ��� @ContextConfiguration({"classpath:spring/spring-dao.xml"})
		  ȥѰ��spring�����ļ���location
		  
		>> @Resource   @Autowired ������ [beanƥ�䷽ʽ��ͬ: byName  or  byType]
	
	5. Spring����ʽ���� @Transactional
	  (1)����ɱϵͳ�У�һ������������ = ����� + ������ɱ��¼ �������������������ݿ���
	     �����ǵ�����������Ϊ�����������Spring����ʽ����������������ִֻ���˼������
		 ��������ڲ�����ɱ��¼�������ʱ�����쳣����ᵼ�����ݵĲ�һ�¡�����Spring����
		 ʽ�����ע�ⷽʽ������һ�����������񣬳���ʱ���Խ��лع������ݱ���һ�¡�
		 
	  (2) ����:
		<!-- �������������, MyBatisĬ��ʹ�õ���JDBC����������� -->
		<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
			<!-- ע�����ݿ����ӳ�,
				��дʱ�������ʾ��ɫ��dataSource,��Ϊ��ǰ��xml�Ҳ�����bean
				����������ʱSpring��ȥ����spring-dao.xml����,���Գ��򲻻����-->
			<property name="dataSource" ref="dataSource"/>
		</bean>
		<!-- ���û���ע�������ʽ����
			Ĭ��ʹ��ע��ķ�ʽ������������Ϊ-->
		<tx:annotation-driven transaction-manager="transactionManager"/>
	
	6. MD5����(�˽���ֵ�ַ���)
		>> String md5 = DigestUtils.md5DigestAsHex(base.getBytes())
		>> MD5: ���������ݰ���ĳ�ֹ�������128λ�Ĺ�ϣֵ==32λ��16������
		>> �˽�MD5�ĵĴ���ԭ��
			https://www.cnblogs.com/second-tomorrow/p/9129043.html
			https://www.cnblogs.com/qianjinyan/p/10216293.html
		>> ��ֵ: https://libuchao.com/2013/07/05/password-salt
	
	7. Enum��ʹ��
	
	8. ���ɲ�����logback��ӡ��־��Ӧ��

	
����Java�߲�����ɱAPI֮Web��

	1. SpringMVC��ִ������: http://baijiahao.baidu.com/s?id=1599271835307699639&wfr=spider&for=pc
	
	2. SpringMVC��Struts2������[��ڡ����ڷ�������/�࿪����ֵջ+OGNL / ModelAndView + JSTL]
	
	3. ѧϰclasspath���� : https://segmentfault.com/a/1190000015802324
	
	4. ����Ajax:(��jsp��ʹ�õ�script�ű�function()��������ajax������)
		ѧϰAjax : https://www.runoob.com/ajax/ajax-tutorial.html
		�� AJAX = Asynchronous JavaScript and XML���첽�� JavaScript �� XML����
		�� AJAX �����µı�����ԣ�����һ��ʹ�����б�׼���·�����
		�� AJAX �����ŵ����ڲ����¼�������ҳ�������£�������������������ݲ����²�����ҳ���ݡ�
		�� AJAX ����Ҫ�κ���������������Ҫ�û�����JavaScript���������ִ�С�
		
	5. ����Restful���֪���� ��https://www.jianshu.com/p/91600da4df95
	
	6. URL   VS   URI : https://www.cnblogs.com/wuyun-blog/p/5706703.html
	
	7. �ݵ���  vs  ���ݵ��� : 
			https://blog.csdn.net/SasukeN/article/details/80919889?utm_source=blogxgwz2
	
	8. Restful�淶:
		�� GET --> ��ѯ����
		�� POST --> ���/�޸Ĳ���
			<!-- POST �� PUT ������:�������ݵ��Ը����ݵ��ԵĲ�����ֲ��� -->
		�� PUT --> �޸Ĳ���
		�� DELETE --> ɾ������
		
	9. SpringMVC��URL����ƹ淶:
		/ģ��/��Դ/{��ʶ}/����1/����2/...
		/user/{uid}/friends --> �����б�
		/user/{uid}/followers -->��ע���б�
		
	10. json�Ǹ����õ� ? https://baike.baidu.com/item/JSON/2462549?fr=aladdin
	   @RequestMapping�е�produces���� �� https://blog.51cto.com/wangguangshuo/2047667
	
	11. ѧϰResponseBodyע�� : 
		>> ���ص��Ƕ���(json / xml �����ݶ���)
		>> ������ViewResolver
		>> ֱ��д�뵽��������,response��body��
		http://www.cnblogs.com/qiankun-site/p/5774325.html
		
	
	12. @RequestMapping����ѧϰ:
		https://blog.csdn.net/weixin_43453386/article/details/83419060#1value_26
		
	13. Long  VS  long �� https://www.cnblogs.com/likun10579/p/5846686.html
	
	14. Ajax�ӿ� �� json���ݵķ�װ����ô��ɵ� �� 
	
	15. Tomcat����ʱ��BUG:
		(1) web.xml��ƥ���·��/*������-->����Tomcat����Maven-Web��Ŀ�Ĳ���ѧϰ
			web.xmlƥ��·��<url-pattern>ʱ�� '/*' �� '/' ������: 
				https://www.cnblogs.com/zuojunyuan/p/6440055.html
		
		(2) EL���ʽ��ʹ������
		
	16. Jquery��JS������Ҫ������JSǰ����,��������������ʾ���˵���������
	
	17. ���� isNaN(number) : number�����ַ���false,�����ַ���true !
	
	18. �������˵�ʱ����ͻ��˵�ʱ���ǲ�һ���ģ�����
		
		
����Java�߲�����ɱAPI֮�߲����Ż�

	1. ϵͳ�лᷢ���߲������ʵĵ�/��������ȡϵͳʱ�䡢��ɱ�ӿڵ�ַ��ִ����ɱ����
	
	2. �Ż������漰֪ʶ�㣺CDN���桢Redis����(����redis��Ӧ�ó�������Щ)
	
	3. ִ����ɱ�߼�������������߳ɱ����� -- > (QPS���ֲ�ʽMQ)
		(F:\Project_Space\Redis�߲�����ɱϵͳ\֪ʶ�㲶׽ͼ��)
		
	4. Ϊʲô��ʹ�� [ Spring����ʽ���� + MySQL ] ���������ݿ� ?
		(1) java����������Ϊ���� ��(F:\Project_Space\Redis�߲�����ɱϵͳ\֪ʶ�㲶׽ͼ��)
		(2) ƿ����������Ҫ�������ӳٸ�GC��ʱ���˷ѣ�����MySQL���ݿⱾ���ִ����
		(3) �Ż������������м����ĳ���ʱ�䣬ʹ��update���������commit/rollback
		
	5. �Ż�˼·���ѿͻ��˵��߼��ŵ�MySQL����ˣ����������ӳٺ�GC
		>> ��ô�ţ�
		>> �洢���̣���MySQL�������������������ǿͻ���������������Ϊ
		>> MySQL�Ǻܸ�Ч��
		
	6. �Ż��ܽ�
		>> ǰ�˿��ƣ���¶�ӿڡ���ť���ظ�
		>> ����̬���ݷ��룺CDN���桢���redis����
		>> �������Ż�������������ʱ��[MySQL�������� + �洢����]
		
	7. protostuff�����л������ʹ��&�ŵ����(��ʡ���л��Ŀռ� + ���л��ٶȿ�)
	
	8. RuntimeSchema
	
	9. Redis�����ӳ�ʱBUG��0.0.0.0
	
	10. ��Redis������ͬ����MySQL��
	
	11. >> ��ɱ�����Ż�1�������м�������ʱ��-->����update��insert��ִ��˳��
		   insert��ʱ����Ҫ��ȡ�м�������ס��һЩ�ظ�����ɱ����ʹ�м�����
		   ����ʱ���֮ǰ��2��ת��Ϊ1��(��Ȼ��spring��������ʲôʱ��ʼrollback ???)
		   
		(����Ż���SQL��MySQL��ִ�� + �洢����)
		>> ��ɱ�����Ż�2�����ô洢����
		
	12. delimiter $$
		>> https://www.cnblogs.com/rootq/archive/2009/05/27/1490523.html
	
	13. Ϊʲô������ɱ�Ķ�MySQL�Ĳ���[update + insert]�ŵ�redis��ִ�У�
	
	14. ��Ŀ��û����ʾ�õ����̵߳ĵط�
		
	