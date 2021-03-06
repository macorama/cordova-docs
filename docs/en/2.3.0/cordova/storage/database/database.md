---
license: Licensed to the Apache Software Foundation (ASF) under one
         or more contributor license agreements.  See the NOTICE file
         distributed with this work for additional information
         regarding copyright ownership.  The ASF licenses this file
         to you under the Apache License, Version 2.0 (the
         "License"); you may not use this file except in compliance
         with the License.  You may obtain a copy of the License at

           http://www.apache.org/licenses/LICENSE-2.0

         Unless required by applicable law or agreed to in writing,
         software distributed under the License is distributed on an
         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
         KIND, either express or implied.  See the License for the
         specific language governing permissions and limitations
         under the License.
---

Database
=======

Contains methods that allow the user to manipulate the Database

Methods
-------

- __transaction__: Runs a database transaction. 
- __changeVersion__: method allows scripts to atomically verify the version number and change it at the same time as doing a schema update. 

Details
-------

A Database object is returned from a call to `window.openDatabase()`.

Supported Platforms
-------------------

- Android
- BlackBerry WebWorks (OS 6.0 and higher)
- iPhone
- webOS
- Tizen

Transaction Quick Example
------------------
	function populateDB(tx) {
		 tx.executeSql('DROP TABLE IF EXISTS DEMO');
		 tx.executeSql('CREATE TABLE IF NOT EXISTS DEMO (id unique, data)');
		 tx.executeSql('INSERT INTO DEMO (id, data) VALUES (1, "First row")');
		 tx.executeSql('INSERT INTO DEMO (id, data) VALUES (2, "Second row")');
	}
	
	function errorCB(err) {
		alert("Error processing SQL: "+err.code);
	}
	
	function successCB() {
		alert("success!");
	}
	
	var db = window.openDatabase("Database", "1.0", "Cordova Demo", 200000);
	db.transaction(populateDB, errorCB, successCB);

Change Version Quick Example
-------------------

	var db = window.openDatabase("Database", "1.0", "Cordova Demo", 200000);
	db.changeVersion("1.0", "1.1");

Full Example
------------

    <!DOCTYPE html>
    <html>
      <head>
        <title>Storage Example</title>

        <script type="text/javascript" charset="utf-8" src="cordova-2.3.0.js"></script>
        <script type="text/javascript" charset="utf-8">

        // Wait for Cordova to load
        //
        document.addEventListener("deviceready", onDeviceReady, false);

        // Cordova is ready
        //
        function onDeviceReady() {
			var db = window.openDatabase("Database", "1.0", "Cordova Demo", 200000);
			db.transaction(populateDB, errorCB, successCB);
        }
		
		// Populate the database 
		//
		function populateDB(tx) {
			 tx.executeSql('DROP TABLE IF EXISTS DEMO');
			 tx.executeSql('CREATE TABLE IF NOT EXISTS DEMO (id unique, data)');
			 tx.executeSql('INSERT INTO DEMO (id, data) VALUES (1, "First row")');
			 tx.executeSql('INSERT INTO DEMO (id, data) VALUES (2, "Second row")');
		}
		
		// Transaction error callback
		//
		function errorCB(tx, err) {
			alert("Error processing SQL: "+err);
		}
		
		// Transaction success callback
		//
		function successCB() {
			alert("success!");
		}
	
        </script>
      </head>
      <body>
        <h1>Example</h1>
        <p>Database</p>
      </body>
    </html>

