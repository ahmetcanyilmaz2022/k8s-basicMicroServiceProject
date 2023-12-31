# k8s-basicMicroServiceProject
mikroservisi anlama adına basit uygulama 

#TEMEL KAVRAMA AÇISINDAN FAYDALI OLACAKTIR 

![image](https://github.com/ahmetcanyilmaz2022/k8s-basicMicroServiceProject/assets/121444420/f8e1a123-4c55-4cb8-9095-d09bdf1f8edf)


web application. We will then try and deploy this web application on multiple
different kubernetes platforms.

Let us now improvise our setup using Deployments. We chose deployments over
ReplicaSets as Deployments automatically create replica sets as required and it can
help us perform rolling updates and roll backs etc. Deployments are the way to go. So
we add more PODs for the front end applications voting-app and result-app by
creating a deployment with 3 replicas. We also encapsulate database and workers in

Let us now focus on the front end applications – voting-app and result-app. We know
that these PODs are hosted on different Nodes. The services with type NodePOrt help
in receiving traffic on the ports on the Nodes and routing and load balancing them to
appropriate PODs. But what IP address would you give your end users to access the
applications. You could access any of these two applications using IP of any of the
Nodes and the high end port the service is exposed on. That would be 4 IP and port
combination for the voting-app and 4 IP and port combination for the result-app. But
that’s not what the end users want. They need a single URL like example-vote.com or
example-result.com. One way to achieve this in my current VirtualBox setup is to
create a new VM for Load Balancer purpose and install and configure a suitable load
balancer on it like HAProxy or NGINX etc. The load balancer would then re-route
traffic to underlying nodes and then through to PODs to serve the users.

![image](https://github.com/ahmetcanyilmaz2022/k8s-basicMicroServiceProject/assets/121444420/1d2d0255-7e6f-412c-86ff-d4e4f52263b2)

![image](https://github.com/ahmetcanyilmaz2022/k8s-basicMicroServiceProject/assets/121444420/2217fe60-cccd-4e12-ac8b-8a85cfcfb3e4)

k8s STEPS:
1 dEPLOY PODS
2  CREATE CLUSTER IP SERVİCES 
REDİS DB
3 CRETAE NODEPORT DERVİCES
VOTİNG-APP
RESULT-APP


#POD İMAGE:result-app
kodekloud/examplevotingapp_result:v1

#POD İMAGE : worker
kodekloud/examplevotingapp_worker:v1

#POD İMAGE : voting-app 
kodekloud/examplevotingapp_vote:v1









DOCKER COMMAND WİTH İMPERATİVE METHOD  



--------------------------------------------------------------------------------------------------------------------------------------------------
voting-app
------------------------------------------
def get_reDis():
    if not hassattr(g, 2redis2):
      g.redis = Redis(host="redis", db=0, socket_timeout=5)
   return g.redis
-------------------------------------------    =======>>>>>>>>>>redis konteyner eşleşme sağlanmalı
pg.connect(postgres://postgre@db/postgres" , function(err, client, done) {
    if (err) {
      console.error("Waiting for db");
    }
    callback(err, client);
    });
----------------------------------------------============>>>>>>>>>db container result app iletişimi eşleşme sağlanmalı 

try {
  Jedis redis = connectToRedis("redis");
  Connection dbConn = connectToDB("DB");

  System.err.printin("Waching vote queu");
------------------------------------------==========>>>>>> postgre db ve redis in worker ile ara bağlamının sağlanması 

--------------------------------------------------------------------------------------------------------------------------------------------------------






***imperative command:

docker run --links
-----

docker run -d --name=redis redis       port =6379

docker run -d --name=redis postgres:9.4         PORT =5432

docker run -d --name=vote -p 5000:80 --link redis:redis voting-app     # --link redis:redis voting app uygulamayı redis konteynera bğlama amaç    PORT = 80

docker run -d --name=result -p 5001:80 --iink db:db result-app          # --link db:db db ile result app bağlantısını amaç.lar       PORT =80

docker run -d --name=worker --link redis:redis worker                   # --link redis:redis worker redis iletiğimi sağlandı  


