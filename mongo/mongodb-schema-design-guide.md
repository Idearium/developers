# Guide on MongoDB schema design

## Three basic ways to model "One-to-N" relationships

Characterize your “One-to-N” relationship with a bit more nuance: is it “one-to-few”, “one-to-many”, or “one-to-squillions”? Depending on which one it is, you’d use a different format to model the relationship.

### Basics: One-to-Few
This is a goose use case for __"embedding"__ array of sub-documents into the parent document.
An example of “one-to-few” might be the addresses for a person.
you’d put the addresses in an array inside of your Person object:
```
> db.person.findOne()
{
  name: 'name',
  addresses : [
     { street: 'street1', city: 'city1', country: 'country1' },
     { street: 'street2', city: 'city2', country: 'country2' }
  ]
}
```

### Basics: One-to-Many
An example of “one-to-many” might be a Product has many parts (several hundreds).
This is a good use case for referencing – you’d put the ObjectIDs of the parts in an array in product document.

Each Part would have its own document:
```
> db.parts.findOne()
{
    _id : ObjectID('AAAA'),
    partno : '123-aff-456',
    name : '#4 grommet',
    qty: 94,
    cost: 0.94,
    price: 3.99
}
```

Each Product would have its own document, which would contain an array of ObjectID references to the Parts that make up that Product:
```
> db.products.findOne()
{
    name : 'left-handed smoke shifter',
    manufacturer : 'Acme Corp',
    catalog_number: 1234,
    parts : [     // array of references to Part documents
        ObjectID('AAAA'),    // reference to the #4 grommet above
        ObjectID('F17C'),    // reference to a different Part
        ObjectID('D2AA'),
        // etc
    ]

```

### Basics: One-to-Squillions
An example of “one-to-squillions” might be an event logging system that collects log messages for different machines.

This is the classic use case for “parent-referencing” – you’d have a document for the host, and then store the ObjectID of the host in the documents for the log messages.

```
> db.hosts.findOne()
{
    _id : ObjectID('AAAB'),
    name : 'goofy.example.com',
    ipaddr : '127.66.66.66'
}

>db.logmsg.findOne()
{
    time : ISODate("2014-03-28T09:42:41.382Z"),
    message : 'cpu is on fire!',
    host: ObjectID('AAAB')       // Reference to the Host document
}
```
