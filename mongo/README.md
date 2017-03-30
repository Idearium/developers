# MongoDB

We use MongoDB to store data for NodeJS applications.

 - [MongoDB Schema design guide](./mongodb-schema-design-guide.md)
 - [MongoDB optimisation guide](./mongodb-optimisation-guide.md)

## Why MongoDB
 - MongoDB stores data using a flexible document data model that is similar to JSON
 - Documents contain one or more fields, including arrays, binary data and sub-documents. Fields can vary from document to document.
 - This flexibility allows development teams to evolve the data model rapidly as the application requirements change
 - Rich, idiomatic drivers are available in all popular programming languages to access documents from MongoDB
 - Documents map naturally to the objects in modern languages
 - MongoDB provides auto-sharding for horizontal scale out.
 - MongoDB makes extensive use of RAM, providing in-memory speed and on-disk capacity
 - MongoDB provides comprehensive secondary indexes, including geospatial and text search, as well as extensive security and aggregation capabilities

## Mongoose

 We use Mongoose - a mongodb object modeling tool for NodeJS.
