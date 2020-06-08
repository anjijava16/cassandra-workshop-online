#Cassandra 

Basic Data Types
text --> UTF-8 encoded String,archar is same as text 
int 
timestamp 

UUID : universally unique identifieer 
Generate via uuid()

timeuuid : now() (Sorable)

CREATE TABLE users (
user_id text ,
name text ,
state text ,
primary key(user_id)
)

INSERT INTO uers VALUES(2,'AADA','CA')

CREATE KEYSPACE “welcome”
WITH replication = {'class': ‘Strategy name’, 'replication_factor' : ‘No.Of   replicas’};

CREATE KEYSPACE welcome
WITH replication = {'class':'SimpleStrategy', 'replication_factor' : 3};

insert into users(user_id,name,state) values('5','afd','ccs');

clustering columns default asending order 
change ordering direction via with clustering order by 


=================================================

CREATE TABLE users_cluster (
state text ,
city text ,
name  text ,
id uuid ,
primary key((state),city,name ,id))
with clustering order by (city desc, name asc );

insert into users_cluster(name,state,city,id) values('newark','DE','1',uuid());


###############################################

# Allow Filtering ::
Allow Filtering relaxes the querying on partition key constraint
You can query on just clusering columns
causes cassandra to scan all parititons in the table 


cqlsh:welcome> select * from users where name ='afd';
InvalidRequest: Error from server: code=2200 [Invalid query] message="Cannot execute this query as it might involve data filtering and thus may have unpredictable performance. If you want to execute this query despite the performance unpredictability, use ALLOW FILTERING"
cqlsh:welcome> select * from users where name ='afd' allow filtering;


select * from users where user_id='6'



Cluster cluster =Cluster.builder().addContactPoint("localhost").build()
Session session=cluster.connect("killervideoKeySpace")
Resultset rs=session.execute("<query ">)
#Python
from cassandra.cluster import cluster 
cluster =Cluster()
session=cluster.connect('killervideoKeySpace')
result=session.execute("<query">)[0]


session.execute(" INSERT .INTO ")


# Node: (java Process JVM)

Node can run any where (




## Drivers :

TokenAwarePolicy ---> Driver choose node which contains the data 
RoundRobinPolicy ---> driver round robins the ring 
DCAwareRoundRobinPolicy  --> driver round robins the target data center 

Client ---> Router ---Leader -- Followers 


VNode :

Adding or removing nodes with vnodes should not make the cluster unblanced
By default each node has 256 vnodes 
vnodes automate token range assignment 



Gossip:
 Cluster metadata :
    Endpoint state 
	  Hearbeat State :
	     generation=5
		 version=22
		 Application state :
		   Status=normal
		   DC=dc-west
		   RACK=rack1
		   LOAD
		   Schema
		   Severity
		   etc
		   


Snitch:
		   EC2Snitch
		   
Simple Strategy 


Network Topology strategy

create keyspace killervideoKeySpac
with replication={
'class':'Network To
}	


Consistency Level :
 RF =3 
CL=QUORUM
CL=ALLOW


WRITE CL=ALL

READ CL =ONE 


QUORUM  VS LOCAL_QUORUM 

# Read Replication ::

CL =ALL


 
		   
Commit Log ---> HDD

MemTable ---> RAM 