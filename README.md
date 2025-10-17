# CNP Server
Commodore Network Protocol Server

This is the Commodore Network Protocol server, which is used to allow the C64 OS network stack to bridge to the internet.

Version 1.5 adds several important features.

- Ability to pause and resume sockets (in use by C64 OS v1.08)
- CNP event logging (events can be viewed from account at c64os.com)
- Added packet acknowledgement timeouts, for packet resending.
- This version switches from using "require" to using "import" for node modules.

## MySQL

A MySQL database is used to store the users and their CNP username and password hash. When users attempt to sign in from C64 OS, the CNP server is authenticating them against the users stored in the users table.

The name, email, address, country and country_code are not technically used by CNP server v1.5, but have planned usage ver CNP server v2.0.

Connections to the CNP server, as well as disconnections of different types, timeouts, signouts, etc. are logged in the cnphistory table.

- users
	- userid
	- name
	- cnpusername
	- cnppwordsalt
	- cnppwordhash

- cnphistory
	- cnphistoryid
	- userid
	- eventdate
	- eventtype
	- ipaddress
	
```	
CREATE TABLE `users` (
  `userid` int NOT NULL AUTO_INCREMENT,
  `name` varchar(128) DEFAULT NULL,
  `email` varchar(128) DEFAULT NULL,
  `address` varchar(255) DEFAULT NULL,
  `country` varchar(128) DEFAULT NULL,
  `country_code` varchar(128) DEFAULT NULL,
  `timezone` varchar(128) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci DEFAULT NULL,
  `cnpusername` varchar(16) DEFAULT NULL,
  `cnppwordsalt` varchar(128) DEFAULT NULL,
  `cnppwordhash` varchar(128) DEFAULT NULL,
  PRIMARY KEY (`userid`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb3	
	
CREATE TABLE `cnphistory` (
  `cnphistoryid` int NOT NULL AUTO_INCREMENT,
  `userid` int DEFAULT NULL,
  `eventdate` datetime DEFAULT NULL,
  `eventtype` int DEFAULT NULL,
  `ipaddress` varchar(128) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci DEFAULT NULL,
  PRIMARY KEY (`cnphistoryid`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb3
```

## NodeJS

The CNP server has been tested to run on node v16.20.2
