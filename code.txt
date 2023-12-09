bid number(5)NOT NULL PRIMARY KEY,
bname varchar(20) );
--Table created.

SQL> create table in_user(
user_id varchar(20)NOT NULL PRIMARY KEY,
name varchar(20),
password varchar(20),
last_login timestamp,
user_type varchar(10)
);
--Table created.

SQL> create table categories(
cid number(5) NOT NULL PRIMARY KEY,
category_name varchar(20));
--Table created.

SQL>create table product(
 pid number(5) primary key,
cid number(5) references categories(cid),
 bid number(5) references brands(bid),
 sid number(5),
 pname varchar(20),
 pstock number(5),
 price number(5),
 added_date timestamp);
--Table created.


SQL> create table stores(sid number(5),sname varchar(20), address varchar(20), mobno number(10)
);
--Table created.

SQL> alter table stores
add primary key(sid);
-- Table altered.

SQL> alter table product add foreign key(sid)references stores(sid);
--Table altered.

SQL> create table provides(bid number(5)references brands(bid), sid number(5)references stores(sid),discount number(5));
--Table created.

SQL> create table customer_cart( cust_id number(5) primary key,name varchar(20), mobno number(10));
--Table created.

SQL> create table select_product( cust_id number(5) references customer_cart(cust_id), pid number(5)references product(pid), quantity number(4) );
---Table created.

SQL> create table transaction(
 trans_id number(5) primary key,
 total_amount number(5),
 paid number(5),
 gst number(3),
 discount number(5),
 payment_method varchar(10),
 cart_id number(5) references customer_cart(cust_id));
--Table created.

SQL> create table invoice(
 item_no number(5),
 product_name varchar(20),
 quantity number(5),
 net_price number(5),
 transaction_id number(5)references transaction(trans_id)
 );
 

INSERTION:

INSERT INTO BRANDS:

SQL> insert into brands values(1,'adidas');
SQL> insert into brands values(2,'puma');
1 row created.
SQL> insert into brands values(3,'Nike');
1 row created.
SQL> insert into brands values(4,'wrong');
1 row created.
select *from brands

INSERT INTO in_user:
SQL>insert into in_user values('govind@gmail.com','Govind krishna','1000','29-oct-22 10:20','manager');
SQL> insert into in_user values('aryan@gmail.com','Aryan raj','1100','12-oct-22 10:20','owner');
1 row created.
SQL> insert into in_user values('rohit@gmail.com','rohit','1110','28-oct-22 10:20','staff');
1 row created.
select *from in_user
truncate table in_user;

INSERT INTO CATEGORIES:
SQL> insert into categories values(1,'electronics');
1 row created.
SQL> insert into categories values(2,'Clothing');
1 row created.
SQL> insert into categories values(3,'Workout essentials');
1 row created.
select *from categories

INSERT INTO STORE
SQL> insert into stores values(1,'rithuraj','chennai',9177026445);
1 row created.
SQL> insert into stores values(2,'badal kumar','delhi',7895624318);
1 row created.
SQL> insert into stores values(3,'kumar','kochi',8864272141);
1 row created.
select *from stores

INSERT INTO PRODUCT:
SQL> insert into product values(1,2,1,1,'T-Shirt',10,5000,'13-oct-22 1:20');
SQL> insert into product values(2,1,3,2,'Airpods',15,7000,'16-oct-22 1:20'); 
SQL> insert into product values(3,1,2,3,'Smart Watch',7,10000,'19-oct-22 1:20'); 
SQL> insert into product values(4,2,4,1,'Shirt',6,1000,'22-oct-22 1:20'); 
SQL> insert into product values(5,3,1,2,'dumbbells',6,4650,'24-oct-22 1:20');
select *from  product


INSERT INTO PROVIDES:
SQL> insert into provides values(1,1,37);
1 row created.
SQL> insert into provides values(2,3,27);
1 row created.
SQL> insert into provides values(3,2,5);
1 row created.
SQL> insert into provides values(4,1,17);
1 row created.
SQL> insert into provides values(1,2,19);
1 row created.
SQL> insert into provides  values(4,3,20);
1 row created.
select *from provides


INSERT INTO CUSTOMER_CART:
SQL> insert into customer_cart values(1,'Gaurav',5654646447);
SQL> insert into customer_cart values(2,'Bhargav',5431285478);
SQL> insert into customer_cart values(3,'Dev',1235978462);
select *from customer_cart



INSERT INTO SELECT_PRODUCT:
SQL> insert into select_product values(1,1,3);
SQL> insert into select_product values(2,2,4);
SQL> insert into select_product values(3,3,4);
SQL> insert into select_product values(2,4,2);
SQL> insert into select_product values(3,5,2);
select *from select_product



INSERT INTO TRANSACTIONS:
insert into transaction values(1,46789,46789,675,600,'cash',1);
insert into transaction values(2,4634,4634,200,150,'upi',2);
insert into transaction values(3,15000,14000,190,100,'cash',3);
select *from transaction

INSERT INTO invoice:

insert into invoice values(1,'Smart watch',5,50000,1);
insert into invoice values(2,'Shirt'4,4000,2);
insert into invoice values(3,'Airpods',2,14000,3);
select * from invoice
SELECT SUM(Price)
FROM invoice;
SELECT SUM(quantity)
FROM invoice;
SELECT count(pid)
FROM product;
SELECT count(trans_id)
FROM transaction;

declare
s number;
n varchar(50);
m number;
d number;
f number;
q number;
c number;
j number;
begin
n:=:name;
m:=:number;
select count(pid) into j from product;
select SUM(Price) into s from invoice;
select SUM(quantity) into q from invoice;
select count(trans_id) into c from transaction;
d := s*15/100;
f := s - d;
dbms_output.put_line('oraganisation name = '||n); 
dbms_output.put_line('gst number = '||m);
dbms_output.put_line('total number of transaction = '||c);
dbms_output.put_line('Total Price of things selled = '||s);
dbms_output.put_line('After Discount = '||f);
dbms_output.put_line('total quantity of products = '||q);
dbms_output.put_line('total number of products = '||j);
end;
