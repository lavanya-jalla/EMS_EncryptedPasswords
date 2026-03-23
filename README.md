## Spring Boot REST API with JDBC Authentication (BCrypt Passwords)
This Spring Boot project demonstrates a secured REST API using Spring Security + JDBC Authentication.
User credentials and roles are stored in a MySQL database, and all passwords are stored using BCrypt hashing (recommended for production).

## BCrypt Password Encryption

 generated encoded passwords using:
 
https://www.javainuse.com/onlineBcrypt

## Database Schema

users table

CREATE TABLE users (

  username VARCHAR(50) NOT NULL PRIMARY KEY,
  
  password VARCHAR(200) NOT NULL,
  
  enabled TINYINT NOT NULL
);

authorities table

CREATE TABLE authorities (

  username VARCHAR(50) NOT NULL,
  
  authority VARCHAR(50) NOT NULL,
  
  CONSTRAINT fk_user FOREIGN KEY (username) REFERENCES users(username)
);

CREATE UNIQUE INDEX ix_auth_username ON authorities(username, authority);

## Insert BCrypt Hashed Users

INSERT INTO users VALUES

('ram', '{bcrypt}$2a$10$XXXXXXXXXX', 1),

('siya', '{bcrypt}$2a$10$YYYYYYYYYY', 1),

('krish', '{bcrypt}$2a$10$ZZZZZZZZZZ', 1);

INSERT INTO authorities VALUES

('ram', 'ROLE_EMPLOYEE'),

('siya', 'ROLE_EMPLOYEE'),

('siya', 'ROLE_MANAGER'),

('krish', 'ROLE_EMPLOYEE'),

('krish', 'ROLE_MANAGER'),

('krish', 'ROLE_ADMIN');

Replace XXXXXXXXXX, YYYYYYYYYY, ZZZZZZZZZZ with actual BCrypt hashes.

## Testing the API

GET (EMPLOYEE)
GET http://localhost:8080/api/employees

POST (MANAGER)
POST http://localhost:8080/api/employees

DELETE (ADMIN)
DELETE http://localhost:8080/api/employees/1

## Author

Lavanya Jalla
