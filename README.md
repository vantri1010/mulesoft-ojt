**Final Assignment** 

Customer want to build the middleware system to transform the data to standard model then store them in the database. 

1. **General Information** 

Using Mulesoft to create and export API following API-led Connectivity Model: 

- Process API will transform message to standard model 
- System API will direct connect with PostgreSQL Database 

![Mulesoft Architecture](https://github.com/vantri1010/mulesoft-ojt/assets/31728513/4873badc-850d-4b10-8aaa-2fc867ac2137)

- **Mapping table**:** 



|**MS1** |**Standard model** |**Database fields** |
| - | - | - |
|**id** |**itemId** |**item\_id** |
|[MS1] |sourceSystem |source\_system |
|[Tracking] |ids.**type** |ids\_type |
|ship\_unit\_barcode |ids.**value** |ids\_value |
|item\_date |itemDate |item\_date |
|event\_type |itemCode |item\_code |
|event\_description |itemDescription |item\_description |
|reason\_id |reason.**code** |reason\_code |
|reason\_text |reason.**text** |reason\_text |
|reason\_description |reason.**description** |reason\_description |
|transport\_id |shipmentId |shipment\_id |
|gps.**lat** |gps.**latitude** |gps\_latitude |
|gps.**long** |gps.**longitude** |gps\_longitude |
|event\_timestamp |captureDate |capture\_date |

1. ***Process Service*** 

**Requirements**: 

- Process service will expose API for client to send the message  
- The API must have match condition below: 
+ API must have clear Raml file  
+ API must have path **/items**, the method allow is **POST.** 
+ Body and Responses must be defined. 
+ API need to check existing record before insert new into the database. If the record already existed 

that record need to be updated 

+ Using Dataweave to transform the message following the dataType 
+ Have Log to show the payload** 

**MS1 DataType**:** 



|**Column Name** |**Type** |**Mandatory / Optional** |
| - | - | - |
|id |String |Mandatory |
|ship\_unit\_barcode |String |Mandatory |
|item\_date |String |Mandatory |
|event\_type |String |Optional |
|event\_description |String |Optional |
|reason\_id |String |Optional |
|reason\_text |String |Optional |
|reason\_description |String |Optional |
|transport\_id |String |Optional |
|gps.**lat** |String |Mandatory |
|gps.**long** |String |Mandatory |
|event\_timestamp |String |Mandatory |
|location\_id |Integer |Optional |
|comment |String |Optional |

**Standard model DataType:** 



|**Column Name** |**Type** |**Mandatory / Optional** |
| - | - | - |
|itemId |String(36) |Mandatory |
|sourceSystem |String(50) |Optional |
|**ids** |Array Object |Mandatory |
|ids.**type** |String(50) |Optional |
|ids.**value** |String(50) |Mandatory |
|itemDate |datetime |Mandatory |
|itemCode |String(5) |Optional |
|itemDescription |String(100) |Optional |
|**reason** |Object |Optional |
|reason.**code** |String(10) |Optional |
|reason.**text** |String(10) |Optional |
|reason.**description** |String(100) |Optional |
|shipmentId |String(10) |Optional |
|**gps** |Object |Optional |
|gps.**latitude** |Integer |Optional |
|gps.**longitude** |Integer |Optional |
|captureDate |datetime |Mandatory |

2. ***System Service*** 

**Requirements**: 

- System service get data from Database and provide to the Process service 
- The system service will expose 3 APIs: 
  - The API get record from database (get by itemId) 
  - The API insert new record into the database (if data not exist) 
  - The API update the existed record in the database  
- The service must have match conditions below: 
+ Clear Raml file 
+ Body and Responses must be defined. 
+ Have Log to show the payload 
3. ***Database:*** 

**Requirements**:** 

- Using SQL script to create** PostgreSQL database with name **Anie** and table **item** 
- Define the **item** table following the **Item Table DataType** below 

**Item Table DataType**: 



|**Column Name** |**Type** |**Mandatory / Optional** |
| - | - | - |
|item\_id |varchar(36) |Mandatory |
|source\_system |varchar(36) |Optional |
|ids\_type |varchar(50) |Optional |
|ids\_value |varchar(50) |Mandatory |
|item\_date |timestamp |Mandatory |



|item\_code |varchar(5) |Optional |
| - | - | - |
|item\_description |varchar(100) |Optional |
|reason\_code |varchar(10) |Optional |
|reason\_text |varchar(10) |Optional |
|reason\_description |varchar(100) |Optional |
|shipment\_id |varchar(10) |Optional |
|gps\_latitude |Integer |Optional |
|gps\_longitude |Integer |Optional |
|capture\_date |timestamp |Mandatory |

2. **General Requirements:** 
- After finishing your assignment you need to **package your source code** and **send it to the trainer**:  
  - Process Service 
  - System Service 
  - Database script 
- **All systems must be connected and run successfully. If any of the source code got any error while building the source stage you will be failed the assignment**. 
- Demonstration and explain your entire systems.  
