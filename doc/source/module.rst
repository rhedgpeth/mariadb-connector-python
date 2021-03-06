.. _module:

The mariadb module
==================

.. sectionauthor:: Georg Richter <georg@mariadb.com>

.. module:: mariadb


The mariadb module supports the standard defined by DB API 2.0 (PEP-249).

.. function::
    connect(\*\*kwargs)

    Establishes a connection to a database server and returns a new connection
    object.

    The connection parameters have to be provided as a set of keyword arguments.

   The supported connection keywords are:

   - **user** (string): The username used to authenticate with the database server, defaults to current user
   - **pasword** (string): The password of the given user
   - **host** (string): The host name or IP address of the database server
   - **database** (string): The database (schema) name to used when connecting with the database server
   - **unix_socket** (string): The location of the unix socket file to use instead of using an IP port to connect.  If socket authentication is enabled, this can also be used in place of a password.
   - **port** (integer): The port number of the database server. If not specified the default value (=3306) will be used.
   - **connect_timeout** (integer): The connect timeout in seconds
   - **read_timeout** (integer): The read timeout in seconds
   - **write_timeout** (integer): The write timeout in seconds
   - **local_infile** (bool): Enables or disables the use of LOAD DATA LOCAL INFILE statements.
   - **compress** (bool) -- Uses the compressed protocol for client server communication. If the
       server doesn't support compressed protocol, the default protocol will
       be used
   - **init_command** (string): Specifies one or more commands to execute when connecting and reconnecting to the database server.
   - **default_file** (string): Read options from the specified option file. If the file is an empty string, default configuration file(s) will be used
   - **default_group** (string): -- Read options from the specified group
   - **ssl_key** (string): Defines a path to a private key file to use for TLS. This option
       requires that you use the absolute path, not a relative path. The specified key must be in PEM format
   - **ssl_cert** (string): Defines a path to the X509 certificate file to use for TLS.  This option requires that you use the absolute path, not a relative path. The X609 certificate must be in PEM format.
   - **ssl_ca** (string): Defines a path to a PEM file that should contain one or more X509 certificates for trusted Certificate Authorities (CAs) to use for TLS.  This option requires that you use the absolute path, not a relative path.
   - **ssl_capath** (string):  Defines a path to a directory that contains one or more PEM files that contains one X509 certificate for a trusted Certificate Authority (CA)
   - **ssl_cipher** (string):  Defines a list of permitted cipher suites to use for TLS
   - **ssl_crl_path** (string): Defines a path to a PEM file that should contain one or more revoked X509 certificates to use for TLS. This option requires that you use the absolute path, not a relative path.
   - **ssl_verify_server_cert** (bool): Enables server certificate verification.
   - **ssl_enforce** (bool): Always use a secure TLS connection


   :return: Returns a connection or raises an error if the connection between client and server couldn't be established.

   :rtype: mariadb.connection object


   :Example:

   The connection parameters have to be provided as a set of keyword arguments::

      import mariadb

      connection= mariadb.connect(user="myuser", host="localhost", database="test", password="secret")


.. function:: 
    ConnectionPool(\*\*kwargs)

    Creates a connection pool and returns a ConnectionPool object.

    The connection parameters have to be provided as a set of keyword arguments::

       db_conf= {user="myname", password="secret", database="test", host="localhost"};
       pool= mariadb.ConnectionPool(pool_name="pool1", **db_conf)

    Beside pool specific parameter all parameters from connect() are supported.
    The supported pool parameters are:

    - pool_name -- Name of the pool
    - pool_size -- Size of the pool. If this value is not provided, a default size of 5 pool connections will be used.
    - pool_reset -- If set to `True` the connection will be resetted after close() method was called.


.. data:: apilevel

    String constant stating the supported DB API level. The value for `mariadb` is
    ``2.0``.

.. data:: threadsafety

    Integer constant stating the level of thread safety. For `mariadb` the value is 1,
    which means threads can share the module but not the connection.

.. data:: paramstyle

    String constant stating the type of parameter marker. For `mariadb` the value is
    `qmark`. For compatibility reasons `mariadb` also supports the `format` and
    `pyformat` paramstyles with the limitation that they can't be mixed inside a SQL statement.

.. data:: mariadbapi_version

    String constant stating the version of the used MariaDB Connector/C library.


Exceptions
----------

Compliant to DB API 2.0 MariaDB Connector/C provides information about errors
through the following exceptions:

.. exception:: DataError

    Exception raised for errors that are due to problems with the processed data like division by zero, 
    numeric value out of range, etc.

.. exception:: DatabaseError

    Exception raised for errors that are related to the database

.. exception:: InterfaceError

    Exception raised for errors that are related to the database interface
    rather than the database itself.

.. exception:: Warning

    Exception raised for important warnings like data truncations while inserting, etc.

.. exception:: PoolError

    Exception rasied for errors related to ConnectionPool class.

.. exception:: OperationalError

    Exception raised for errors that are related to the database's operation 
    and not necessarily under the control of the programmer

.. exception:: IntegrityError

    Exception raised when the relational integrity of the database is affected, 
    e.g. a foreign key check fails.

.. exception:: InternalError

    Exception raised when the database encounters an internal error, 
    e.g. the cursor is not valid anymore

.. exception:: ProgrammingError

    Exception raised for programming errors, e.g. table not found or already 
    exists, syntax error in the SQL statement

.. exception:: NotSupportedError

    Exception raised in case a method or database API was used which is not
    supported by the database

Type objects and constructors
------------------------------

.. function:: Binary()

   This function constructs an object capable of holding a binary (long)
   string value

.. function:: Date(year, month, day)

    This function constructs an object holding a date value

.. function:: DateFromTicks(ticks)

    This function constructs an object holding a date value from the given
    ticks value (number of seconds since the epoch). For more information
    see the documentation of the standard Python time module
    
.. function::  Time(hour, minute, second)

    This function constructs an object holding a time value
    
.. function::  TimeFromTicks(ticks)

    This function constructs an object holding a time value from the given
    ticks value (number of seconds since the epoch). For more information
    see the documentation of the standard Python time module
    
.. function::  Timestamp(year, month, day, hour, minute, second)

    This function constructs an object holding a time stamp value
    
.. function::  TimestampFromTicks(ticks)

    This function constructs an object holding a time stamp value from the given
    ticks value (number of seconds since the epoch). For more information
    see the documentation of the standard Python time module

.. data:: STRING

    This type object is used to describe columns in a database that are
    string-based (e.g. CHAR).

.. data:: BINARY

    This type object is used to describe (long) binary columns in a database
    (e.g. LONG, RAW, BLOBs).

.. data:: NUMBER

    This type object is used to describe numeric columns in a database.

.. data:: DATETIME

    This type object is used to describe date/time columns in a database.

.. data:: ROWID

    This type object is used to describe the "Row ID" column in a database.

.. data:: indicator_default

    This indicator object is used to use a default value for insert/update.

.. data:: indicator_ignore

    This indicatior object is used to skip the update of a column.

.. data:: indicator_null

    This indicator object is used for NULL values.

.. data:: indicator_row

    This indicator object is used for skip the update/insert of the entire row. 

