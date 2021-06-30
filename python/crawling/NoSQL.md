# NoSQL

 = Not Only SQL

* many different databases that are not related to each other

<실사용예시> 문제해결 실제로 사용하는 방식 보여주고 

어떤 db 많이 사용? Cassandra DB? graph DB 중 하나? 

**document DB**

e.g. mongoDB

- save data as json document (no rows or columns)

- can save any shape or any structure you want 

- flexible

**key value DB**

less freedom 

have to think in advance what are you going to look in the data before you save it

e.g. CassandraDB

* column wide database
* Write and read things very quickly
* Apple, netflix, instagram, uber use this DB

e.g. Dynamo DB

* created by Amazon
* when you have to write a lot, read a lot really quickly

**graph DB**

When you don't need document or columns

but when you need to know the relationship between the nodes

e.g. social network Facebook (Tao)

* store entity and connect them through relationship 
* User1 shared Photo1
* User1 likes User2



really fast <-> can't query things as you do in SQL

So have to think about how your data will be retrieved before you put it in



Batch 저장해놓았다가 한번에 처리?

streaming 실시간으로 처리 