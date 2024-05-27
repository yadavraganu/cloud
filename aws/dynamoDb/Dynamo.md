# What is Dynamo DB?
- Managed NoSQL database optimized for performance at scale
- High availability & durability
- It is ideal for application with known access patterns
- Accessible through APIs & authorized through IAM
- Integrates well with other AWS services
- Cost-effective, usage-based payment model (On-Demand, Provisioned)

# Dynamo Db Components 
__Tables :__ Collection of items.  

__Items :__ Collection of attributes or key-value pair.  

__Primary Key :__ Primary key consists of a partition key & sort key. Both keys combined should be unique but not   
necessarily at individual level.It is not mandate to use sort key.   

__Partition Key :__ It is the part of the table's primary key. It's hash value is used to retrieve the item from the table  
& allocate data across hosts for scalability & availability.  

__Sort Key :__ It can be used as the second part of table's primary key. It allows you to sort or search among all the   
items sharing the same partition key.  

__Secondary Indexes :__ Use secondary indexes to perform queries on attributes that are not part of your table's primary key.

__Global secondary index(GSI) :__ It is key which is used on attributes which are different from a primary key & your  
application performs operations based on these. GSI includes as second partition key as well as optional sort key.  
It has explicit RCU, WCU assigned to it.It has cost associated with it.You can select few required attributes.  
So basically GSI clones your table using new partition & sort key.  
It is eventually consistent so your GSI can return stale data.  

__Local secondary index(LSI) :__ It is a secondary index that is used to find a record within a partition key apart from a sort key.

__Encryption :__ All user data stored in DynamoDB is fully encrypted at rest. By default, DynamoDB manages the   
encryption key & it is free. There are below options available:
- Owned by Amazon DynamoDB(Default Free)
- AWS managed CMK (Charged)
- Stored in your account and owned, managed by you (Charged)

__Capacity Mode :__  
__On-Demand :__ Simplify bills by paying for the actual reads & writes your application performs  
__Provisioned :__ Manage and optimize your costs by allocating read/write capacity in advance.    
__Read capacity (RPU):__ There is an option to autoscale RPUs as well as fixed.  
__Write capacity (WCU):__ There is an option to autoscale WCUs as well as fixed.  
For autoscaling provide min & max units as well target utilization percent

__Import/Export :__
- Data files can be imported from S3
- Dynamo db to S3 export can also be done. 

__TTL :__
- It allows the automatic removal of individual items from table
- Reduces cost & makes some query performant
- Totally free, does not consume WCU .It uses burst capacity
- TTL happens automatically.
- Time must be in epoch.Attribute having this epoch should be of N (Number) type not S (String).
- TTL can take 48 hours or more asynchronously.

__DynamoDB Stream :__
- It emits the events when any kind of record modification happens on the table.
- Events can be of INSERT, UPDATE, DELETE type.
- Events can carry the events of row being modified.
- Events guaranteed to be in the same order as modification took place.
- No performance impact on the table.
- Events can carry data of modified data like (Key only,old data,new data,new & old data).
- Events can be batched when integrating with lambda