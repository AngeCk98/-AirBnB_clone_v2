This repository contains the second version of the project to build a clone of the AirBnB website.

In this version, the front-end is designed using HTML5/CSS3 and is served using Python Flask. The application is configured on a distributed system - two webservers and one load balancer - with Nginx and HAProxy. Also, it integrates file and database (MySQL) storage in a back-end API.

Storage
All classes are handled by one of either two abstracted storage engines, depending on the call - FileStorage or DBStorage.

FileStorage
The default mode.

In FileStorage mode, every time the backend is initialized, the program instantiates an instance of FileStorage called storage. The storage object is loaded/re-loaded from any class instances stored in the JSON file file.json. As class instances are created, updated, or deleted, the storage object is used to register corresponding changes in the file.json.

DBStorage
Run by setting the environmental viriables HBNB_TYPE_STORAGE=db.

In DBStorage mode, every time the back-end is initialized, the program intantiates an instance of DBStorage called storage. The storage object is loaded/re-loaded from the MySQL database specified in the environmental variable HBNB_MYSQL_DB, using the user HBNB_MYSQL_USER, password HBNB_MYSQL_PWD, and host HBNB_MYSQL_HOST. As class instances are created, updated, or deleted, the storage object is used to register changes in the corresponding MySQL database. Connecion and querying is achieved using SQLAlchemy.

Note that the databases specified for DBStorage to connect to must already be defined on the MySQL server. This repository includes scripts setup_mysql_dev.sql and setup_mysql_test.sql to set up hbnb_dev_db and hbnb_test_db databases in a MySQL server, respectively.

Testing
Unittest for this progrem are defined in the test folder. To run the entire test suite simultaneously, execute the following command:

$ python3 unittest -m discover tests
Alternatively, you can specify a single test file to run at a time:

$ python3 -m unittest tests/test_models/test_engine/test_file_storage.p
