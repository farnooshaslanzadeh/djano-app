#  Deploy Wordpress
Wordpress is a CMS system used to publish blog posts. Deploy wordpress and a mysql database to be used by wordpress. 
For this exercise you don’t need to create Dockerfiles. 
# ```docker pull wordpress```
# ```docker run --name local-mysql1 -e MYSQL_ROOT PASSWORD=... -d mysql:5.7```
# ``` docker exec -it local-mysql1 mysql -u root -p```
# ```mysql> create database wordpress```
# ```docker run --name local-mywordpress -p 8082:80 -d wordpress```
# ```docker network create --attachable wordpress-network```
# ```docker network connect wordpress-network local-mysql1```
# ```docker network connect wordpress-network local-mywordpress```
Open your browser and access our wordpress by ```localhost:8082```
