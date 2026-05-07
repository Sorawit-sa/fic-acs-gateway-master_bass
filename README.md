# fic-acs-gateway-master_bass
acs-gateway Integrate ACS KIDDO

Readme : Integrate ACS KIDDO

1.PATH : ACSGateway/src/main/webapp/WEB-INF

-  แก้ไขไฟล์ web.xml  เพิ่ม url ของ kiddo

	<!-- production Kiddo -->
	<context-param>
		<param-name>url.kiddo.prod</param-name>
		<param-value>http://10.235.109.206:9094/kiddoacs</param-value>
	</context-param>

______________________________________________________________________________

2.PATH : ACSGateway/src/main/java/th/co/ais/acs/rest/init/ 

-  แก้ไขไฟล์ InitialParameter.java เพิ่มตัวแปร url_kiddo รับค่า url kiddo จาก web.xml

url_kiddo = context.getInitParameter("url.kiddo.prod");

______________________________________________________________________________

3.PATH : ACSGateway/src/main/java/th/co/ais/acs/rest/log/

- สร้างไฟล์ LogKIDDO.java

______________________________________________________________________________

4.PATH : ACSGateway/src/main/webapp/WEB-INF/etc/

-  แก้ไขไฟล์ log4j2.xml เพิ่ม LogKIDDO

<Logger  name="th.co.ais.acs.rest.log.LogKIDDO" level="info" additivity="true">

<RollingFile name="LogKIDDO-APPENDER" fileName="${logDir}/info/kiddo.log" filePattern="${logDir}/info/kiddo.log.%d{yyyy-MM-dd}.gz">

______________________________________________________________________________

5.PATH : ACSGateway/src/main/java/th/co/ais/acs/rest/impl/

- สร้างไฟล์ KiddoOperation.java (อ้างอิงตาม KIDDO API Spec ลบ method ที่ไม่ได้ใช้ออก)

- สร้างไฟล์ KiddoServiceImpl.java (อ้างอิงตาม KIDDO API Spec method ที่ไม่ได้ใช้ แก้โค้ดไส้ในเป็น return null และย้าย method ลงไปด้านล่าง)

______________________________________________________________________________

6.PATH : ACSGateway/src/main/java/th/co/ais/acs/rest/init/ 

-  แก้ไขไฟล์ InitialParameter.java  เพิ่มการเรียก method KIDDO impl

เพิ่ม public static KiddoOperation getKiddoOperation()
เพิ่ม public static AcsService getKiddoServiceDao()

______________________________________________________________________________

7.PATH : ACSGateway/src/main/java/th/co/ais/acs/rest/restapi/

- แก้ไขไฟล์ ACSRestServiceInfo.java

เพิ่ม AcsService kiddoServiceDao = InitialParameter.getKiddoServiceDao();
เพิ่ม else if (KIDDO) ใน Method public Response getparametervalues( String requestMassage ) 

- แก้ไขไฟล์ ACSRestServiceConf.java

เพิ่ม AcsService kiddoServiceDao = InitialParameter.getKiddoServiceDao();
เพิ่ม else if (KIDDO) ใน Method public Response setparametervalues( String requestMassage ) 

- แก้ไขไฟล์ ACSRestServiceSys.java

เพิ่ม AcsService kiddoServiceDao = InitialParameter.getKiddoServiceDao();
เพิ่ม else if (KIDDO) ใน Method public Response reboot( String requestMassage )



