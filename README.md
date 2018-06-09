# Beego social app server

## Updates
## V. 0.1.2
The first thing is to replace the string type location to a bool type showing if it exists. Another thing is to add foreign key into the table `MOMENT`, so that every moment has its owner. Thus the SQLs for building tables has changed as follows:
```sql
drop table if exists USER;
drop table if exists MOMENT;

create table USER (
   user_id              varchar(12) not null,
   user_name            varchar(20) not null,
   password             varchar(30) not null,
   primary key (user_id)
);
insert into USER 
    values ('12345', 'abc', 'password');

create table MOMENT (
   moment_id            bigint not null,
   moment_time          varchar(128) not null,
   if_tag               bool not null,
   if_text              bool not null,
   if_image             bool not null,
   fk_user_id           varchar(12) not null,
   primary key (moment_id),
   foreign key (fk_user_id) references USER(user_id) on delete cascade
);
insert into MOMENT
    values (1, '2006-01-02 15:04:05', false, false, false, '12345');
```

LEAVE:
1. add USER_PROFILE table
2. support Chinese characters in moment text and tags
3. add FRIEND_LIST table
4. Role based access control(RBAC)

## V. 0.1.1
APIs about moment:
1. Get all moments
2. Post a moment
3. Get a moment by moment id
4. Delete a moment by moment id

APIs about user:
1. Get all users
2. Post a new user
3. Login user
4. Logout user
5. Get a user by user's phone

## V. 0.1.0
1. create two tables named `USER` and `COMMENT`
2. generate an api example from Beego

## Requirements
Development Language: Go 1.10 or higher
Server Framework: Beego 1.9
Database: MySQL (5.6+)
API documentation: Swagger UI
ODBC: go-sql-driver

## SQLs used for building tables
see file *create_db.sql*
