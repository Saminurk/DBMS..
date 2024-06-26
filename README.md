create table branch(branch_name varchar(10),branch_city varchar(10),assets int,primary key(branch_name));

create table account(accno int,branch_name varchar(10),balance int,primarykey(accno),foreign
key(branch_name) references branch(branch_name));

create table customer(customer_name varchar(10),customer_street varchar(10),customer_city
varchar(10),primary key(customer_name));

create table depositor(customer_name varchar(10),accno int,primary
key(customer_name,accno),foreign key(customer_name) references
customer(customer_name),foreign key(accno) references account(accno) on delete cascade);

create table loan(loan_number int,branch_name varchar(10),amount int,primary
key(loan_number),foreign key(branch_name) references branch(branch_name));

create table borrower(customer_name varchar(10),loan_number int,primary
key(customer_name,loan_number),foreign key(customer_name) references
customer(customer_name),foreign key(loan_number) references loan(loan_number));

create table employee(emp_name varchar(20),branch_name varchar(10), salary int, primary
key(emp_name,branch_name), foreign key(branch_name) references branch(branch_name));

insert into branch values(‘Jadavpur’
,’Kolkata’,170000);
insert into customer values(‘Abhilash’,’RTNagar’,’Bangalore’);
insert into account values(1000,’Jadavpur’,50000);
insert into depositor values(‘Abhilash’,1000);
insert into loan values(111,
’Jasola’,800000);
insert into borrower values(‘Amit’,111);
insert into employee values(‘Ajay’,’Jadavpur’,150000);

select customer_name from customer;
select distinct branch_name from loan;
select * from branch;
select accno, balance from account where balance>700;
select * from account where branch_name='Brighton' and balance>800;
select branch_name,assets as 'assets in thousands' from branch;
select branch_name, assets from branch where assets between '1000000' and '4000000';
select c.customer_name,a.accno,a.balance from customer c, account a,depositor d where
c.customer_name=d.customer_name and a.accno=d.accno;
select c.customer_name,a.accno,a.balance from customer c, account a,depositor d where
c.customer_name=d.customer_name and a.accno=d.accno and a.balance<400;
