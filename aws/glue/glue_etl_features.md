# Job bookmarks
Bookmarking is a key feature available in Glue ETL that allows users to keep track of data that was processed and written. During the next job run, only new data will be processed. This is an extremely useful option that helps in processing large datasets that are constantly growing. While specifying the syntax for DynamicFrame creation from the Data Catalog
table earlier, the transformation_ctx parameter was mentioned in the code snippet. This parameter is used as the identifier for the job bookmark’s state, which is persisted across job runs.  
Job bookmarks are supported for S3 and JDBC-based data stores. At the time the JSON, CSV, Apache Avro, XML, Parquet, and ORC file formats are supported with S3 data stores. For an Amazon S3 data source, job bookmarks keep track of the last modified timestamp of the objects processed. This information is then persisted in the bookmark storage on the service side. During the next jobRun, the information that was collected by the bookmark in the previous jobRun will be used to filter out already processed objects; then, new
objects are processed.
NOTE:
A new version of an already existing object is still considered a new object and will be processed in the new jobRun.
At the time of writing, Glue DynamicFrames only support Spark SaveMode.Append mode for writes. So, if a new version of an object was added to the data store, there is a possibility
of data duplication in the target data store. This must be handled by the user with custom logic in the ETL script.  

For JDBC data stores, job bookmarks use key(s) specified by the user and the order of the keys to track the data being processed. If no keys are specified by the user, Glue will use the primary key of the JDBC table. It is important to note that Glue will not accept the primary key, which is not sequential (there shouldn’t be gaps in the values). In such cases, we just
have to specify the column manually as the key in the jobBookmarkKeys parameter in additional_options (connection_options for the from_options API). This will force Glue to use the key for bookmarking.  

If more than one key is specified, Glue will combine the keys to form a single composite key. However, if a key is not specified, Glue will use the primary key of the JDBC table as
the key (only if the key is increasing/decreasing sequentially). If keys are specified by the user, gaps are allowed for these keys. However, the keys have to be sorted – either increasing or decreasing.
