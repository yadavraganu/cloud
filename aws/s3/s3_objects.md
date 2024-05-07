Amazon S3 is an object store that uses unique key-values to store as many objects as you want. You store these objects  
in one or more buckets, and each object can be up to 5 TB in size. An object consists of the following:

### Key
The name that you assign to an object. You use the object key to retrieve the object.

### Version ID
Within a bucket, a key and version ID uniquely identify an object. The version ID is a string that Amazon S3 generates  
when you add an object to a bucket.

### Value
The content that you are storing.  
An object value can be any sequence of bytes. Objects can range in size from zero to 5 TB. 

### Metadata
A set of name-value pairs with which you can store information regarding the object. You can assign metadata, referred  
to as user-defined metadata, to your objects in Amazon S3. Amazon S3 also assigns system-metadata to these objects,  
which it uses for managing objects.

### Subresources
Amazon S3 uses the subresource mechanism to store object-specific additional information. Because sub resources are  
subordinates to objects, they are always associated with some other entity such as an object or a bucket.

### Access control information
You can control access to the objects you store in Amazon S3. Amazon S3 supports both the resource-based access  
control, such as an access control list (ACL) and bucket policies, and user-based access control.