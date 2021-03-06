---

copyright:
  years: 2017,2018
lastupdated: "2018-06-19"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#  Spark connectors
The following connectors are currently provided by default on all {{site.data.keyword.iae_full_notm}} clusters:

 * [Db2 and {{site.data.keyword.dashdbshort_notm}}](#db2-and-db2-warehouse-on-cloud-connector)
  * Db2 JDBC
  * Db2 ODBC
  * {{site.data.keyword.dashdbshort_notm}} Idax Data Source(com.ibm.idax.spark.idaxsource)
 * [Cloudant](#cloudant)

## Db2 and {{site.data.keyword.dashdbshort_notm}} connector

{{site.data.keyword.dashdbshort_notm}} (now also known as dashDB) is a fully managed cloud data warehouse, purpose-built for analytics. It offers massively parallel processing (MPP) scale, and compatibility with a wide range of business intelligence (BI) tools.

### Sample Python code to access {{site.data.keyword.dashdbshort_notm}}  using JDBC

Use the following sample code to access {{site.data.keyword.dashdbshort_notm}} using JDBC:

 ```
credentials_1 = {
'jdbcurl':'jdbc:db2://YOUR_DATABASE_HOSTNAME:50000/YOUR_DATABASE_NAME',
 'username':'YOUR_DATABASE_USERNAME',
 'password':'YOUR_DATABASE_PASSWORD’
}
transportation = sqlContext.read.jdbc(credentials_1["jdbcurl"],"YOUR_DATABASE_TABLE",properties = {"user" : credentials_1["username"], "password" : credentials_1["password"],"driver" : "com.ibm.db2.jcc.DB2Driver"})
transportation.show()
```
{: codeblock}

### Sample Python code to access {{site.data.keyword.dashdbshort_notm}}  using ODBC

Use the following sample code to access {{site.data.keyword.dashdbshort_notm}} using ODBC:

 ```
from ibmdbpy import IdaDataBase, IdaDataFrame
idadb_1 = IdaDataBase(dsn='DASHDB;Database=YOUR_DB_NAME;Hostname=YOUR_DATABASE_HOSTNAME;Port=YOUR_DATABASE_PORT;PROTOCOL=TCPIP;UID= YOUR_DATABASE_USERNAME;PWD= YOUR_DATABASE_PASSWORD')
ida_df_1 = IdaDataFrame(idadb_1, YOUR_DATABASE_TABLE_NAME',indexer="YOUR_TABLE_COLUMN")
ida_df_1.head()
```
{: codeblock}

### Sample Python code to access {{site.data.keyword.dashdbshort_notm}} using the IDAX connector

Use the following code sample to access {{site.data.keyword.dashdbshort_notm}} using the IDAX connector:

 ```
 credentials_1 = {
  'jdbcurl':'jdbc:db2://YOUR_DATABASE_HOSTNAME:50000/YOUR_DATABASE_NAME',
  'username':'YOUR_DATABASE_USERNAME',
  'password':'YOUR_DATABASE_PASSWORD’
  }
  inputData = spark.read.format("com.ibm.idax.spark.idaxsource").options(dbtable="YOUR_TABLE").options(**credentials_1).load()

  print(inputData.show())
```
{: codeblock}


## Cloudant

Sample Python code to access Cloudant:

```
db_name = "YOUR_CLOUDANT_DBNAME"
data_df = sqlContext.read.format("com.cloudant.spark").option("cloudant.host","YOUR_CLOUDANT_USERNAME.cloudant.com").option("cloudant.username"," YOUR_CLOUDANT_USERNAME ").option("cloudant.password"," YOUR_CLOUDANT_PASSWORD
```
{: codeblock}
