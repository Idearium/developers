# Guide on how to optimise MongoDB

### Analyse your Queries
MongoDB provides an explain facility which reveals how a database operation worked. You can add explain('executionStats') to a query. For example:
```
db.user.find(
  { country: 'AU', city: 'Adelaide' }
).explain('executionStats');
```
or append it to the collection:
```
db.user.explain('executionStats').find(
  { country: 'AU', city: 'Adelaide' }
);
```
This returns a large JSON result, but there are two primary values to examine:

`executionStats.nReturned` — the number of documents returned, and
`executionStats.totalDocsExamined` — the number of documents scanned to find the result.

If the number of documents examined greatly exceeds the number returned, the query may not be efficient. In the worst cases, MongoDB might have to scan every document in the collection. The query would therefore benefit from the use of an index.

For more information and examples, refer to [Analyze Query Performance](https://docs.mongodb.com/manual/tutorial/analyze-query-plan/) and [db.collection.explain()](https://docs.mongodb.com/manual/reference/method/db.collection.explain/) in the [MongoDB manual](https://docs.mongodb.com/manual/).

### Add Appropriate Indexes
NoSQL databases require indexes. An index is built from a set of one or more fields to make querying fast. For example, you could index the country field in a user collection. When a query searches for ‘AU’, MongoDB can find it in the index and reference all matching documents without having to scan the entire user collection.

Indexes are created with createIndex. The most basic command to index the country field in the user collection in ascending order:
```
db.user.createIndex({ country: 1 });
```
The majority of your indexes are likely to be single fields, but you can also create compound indexes on two or more fields. For example:
```
db.user.createIndex({ country: 1, city: 1 });
```
There are many indexing options, so refer to the MongoDB manual [Index](https://docs.mongodb.com/manual/indexes/) for more information.

### Query Selectivity
Query selectivity refers to how well the query predicate excludes or filters out documents in a collection. Query selectivity can determine whether or not queries can use indexes effectively or even use indexes at all.

More selective queries match a smaller percentage of documents. For instance, an equality match on the unique `_id` field is highly selective as it can match at most one document.

Less selective queries match a larger percentage of documents. Less selective queries cannot use indexes effectively or even at all.

For instance, the inequality operators `$nin` and `$ne` are not very selective since they often match a large portion of the index. As a result, in many cases, a `$nin` or `$ne` query with an index may perform no better than a `$nin` or `$ne` query that must scan all documents in a collection.

### Limit the Number of Query Results to Reduce Network Demand
MongoDB cursors return results in groups of multiple documents. If you know the number of results you want, you can reduce the demand on network resources by issuing the limit() method.

This is typically used in conjunction with sort operations. For example, if you need only 10 results from your query to the posts collection, you would issue the following command:

```
db.posts.find().sort( { timestamp : -1 } ).limit(10)
```
For more information on limiting results, see [limit()](https://docs.mongodb.com/manual/reference/method/cursor.limit/#cursor.limit)

### Use Projections to Return Only Necessary Data
When you need only a subset of fields from documents, you can achieve better performance by returning only the fields you need:

For example, if in your query to the posts collection, you need only the timestamp, title, author, and abstract fields, you would issue the following command:
```
db.posts.find( {}, { timestamp : 1 , title : 1 , author : 1 , abstract : 1} ).sort( { timestamp : -1 } )
```
For more information on using projections, see [Project Fields to Return from Query](https://docs.mongodb.com/manual/tutorial/project-fields-from-query-results/#read-operations-projection).

### Be Wary When Sorting
You almost certainly want to sort results, e.g. return all users in ascending country-code order:

```
db.user.find().sort({ country: 1 });
```

Sorting works effectively when you have an index defined. Either the single or compound index defined above would be suitable.

If you don’t have an index defined, MongoDB must sort the result itself, and this can be problematic when analysing a large set of returned documents.

### Use lean where possilbe
Documents returned from queries with the lean option true are plain javascript objects, not Mongoose Documents. They have no save method, getters/setters or other Mongoose magic applied. So in this way the over head attached to the mongoose document is not there in case of lean and we get high performance.
For example:
```
User.find(
  { country: 'AU', city: 'Adelaide' }
).lean().exec((err, users) => {
  .......
  })
```

### Create Two or More Connection Objects
When building an application, you can increase efficiency with a single persistent database connection object which is reused for all queries and updates.

MongoDB runs all commands in the order it receives them from each client connection. While your application may make asynchronous calls to the database, every command is synchronously queued and must complete before the next can be processed. If you have a complex query which takes ten seconds to run, no one else can interact your application at the same time on the same connection.

Performance can be improved by defining more than one database connection object. For example:

- one to handle the majority of fast queries
- one to handle slower document inserts and updates
- one to handle complex report generation.

Each object is treated as a separate database client and will not delay the processing of others. The application should remain responsive.

## Set Maximum Execution Times
MongoDB commands run as long as they need. A slowly-executing query can hold up others, and your web application may eventually time out. This can throw various strange instability problems in Node.js programs, which happily continue to wait for an asynchronous callback.

You can specify a time limit in milliseconds using maxTimeMS(): for example, permit 100 milliseconds (one tenth of a second) to query documents in the user collection where the city fields starting with the letter ‘A’:

```
db.user.find({ city: /^A.+/i }).maxTimeMS(100);
```

You should set a reasonable maxTimeMS value for any command which is likely to take considerable time. Unfortunately, MongoDB doesn’t allow you to define a global timeout value, and it must be set for individual queries (although some libraries may apply a default automatically).

## Rebuild your Indexes
If you’re satisfied your structure is efficient yet queries are still running slowly, you could try rebuilding indexes on each collection. For example, rebuild the user collection indexes from the mongo command line:

```
db.user.reIndex();
```
