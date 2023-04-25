# Oracle-Confluent-MongoDB-GraphQL
Learn how to update a legacy Oracle system by using GraphQL to update a MongoDB collection. Have that collection read by Confluent to update a series of legacy Oracle tables.

MongoDB GraphQL Documentation.  
[https://www.mongodb.com/docs/atlas/app-services/graphql/](https://www.mongodb.com/docs/atlas/app-services/graphql/).  
[https://www.mongodb.com/developer/products/realm/graphql-easy/](https://www.mongodb.com/developer/products/realm/graphql-easy/).    
[https://www.mongodb.com/docs/atlas/app-services/graphql/cli/](https://www.mongodb.com/docs/atlas/app-services/graphql/cli/).     
[https://www.mongodb.com/docs/atlas/app-services/graphql/authenticate/](https://www.mongodb.com/docs/atlas/app-services/graphql/authenticate/)

### Next GEN POS Order Examples

```JSON
{
  "_id":{"$oid":"6439fe117ec419fd7f5e88a8"},
  "CUSTOMER_ID":{"$numberLong":"146"},
  "EMAIL_ADDRESS":"rey.wada@internalmail",
  "FULL_NAME":"Rey Wada",
  "STORE_ID":{"$numberLong":"4"},
  "STORE_NAME":"New York City",
  "ORDER_DATETIME":{"$date":{"$numberLong":"1680779156000"}},
  "ORDER_STATUS":"COMPLETE","ORDER_TOTAL":{"$numberDouble":"82.41"},
  "PRODUCT_LIST":[
    {"PRODUCT_ID":{"$numberLong":"19"},"PRDOUCT_NAME":"Men's Coat (Red)","UNIT_PRICE":{"$numberDouble":"28.21"}},
    {"PRODUCT_ID":{"$numberLong":"28"},"PRODUCT_NAME":"Men's Hoodie (Red)","UNIT_PRICE":{"$numberDouble":"24.71"}},
    {"PRODUCT_ID":{"$numberLong":"9"},"PRODUCT_NAME":"Women's Jeans (Brown)","UNIT_PRICE":{"$numberDouble":"29.49"}}
    ]
}

{
  "_id":{"$oid":"64398a780c4e4d07cf6eacb6"},
  "CUSTOMER_ID":{"$numberLong":"139"},
  "EMAIL_ADDRESS":"elaine.moncure@internalmail",
  "FULL_NAME":"Elaine Moncure",
  "STORE_ID":{"$numberLong":"3"},
  "STORE_NAME":"Seattle",
  "ORDER_DATETIME":{"$date":{"$numberLong":"1680779156000"}},
  "ORDER_STATUS":"COMPLETE","ORDER_TOTAL":{"$numberDouble":"52.92"},
  "PRODUCT_LIST":[
    {"PRODUCT_ID":{"$numberLong":"19"},"PRDOUCT_NAME":"Men's Coat (Red)","UNIT_PRICE":{"$numberDouble":"28.21"}},
    {"PRODUCT_ID":{"$numberLong":"28"},"PRODUCT_NAME":"Men's Hoodie (Red)","UNIT_PRICE":{"$numberDouble":"24.71"}}
    ]
}

```


### GraphQL Schema
```JSON
{
  "title": "NgPosCustomerOrder",
  "properties": {
    "CUSTOMER_ID": {
      "bsonType": "long"
    },
    "EMAIL_ADDRESS": {
      "bsonType": "string"
    },
    "FULL_NAME": {
      "bsonType": "string"
    },
    "ORDER_DATETIME": {
      "bsonType": "date"
    },
    "ORDER_STATUS": {
      "bsonType": "string"
    },
    "ORDER_TOTAL": {
      "bsonType": "double"
    },
    "PRODUCT_LIST": {
      "bsonType": "array",
      "items": {
        "bsonType": "object",
        "properties": {
          "PRODUCT_ID": {
            "bsonType": "long"
          },
          "PRODUCT_NAME": {
            "bsonType": "string"
          },
          "UNIT_PRICE": {
            "bsonType": "double"
          }
        }
      }
    },
    "STORE_ID": {
      "bsonType": "long"
    },
    "STORE_NAME": {
      "bsonType": "string"
    },
    "_id": {
      "bsonType": "objectId"
    }
  }
}
```
[https://realm.mongodb.com/groups/641519d8f14d271731440d7a/apps/643a013931a8f6ef9a5917cd/sdks](https://realm.mongodb.com/groups/641519d8f14d271731440d7a/apps/643a013931a8f6ef9a5917cd/sdks)
[https://learning.postman.com/docs/sending-requests/graphql/graphql/](https://learning.postman.com/docs/sending-requests/graphql/graphql/)

```js
query {
  ngPosCustomerOrders {
    CUSTOMER_ID
		EMAIL_ADDRESS
		FULL_NAME
		ORDER_DATETIME
		ORDER_STATUS
		ORDER_TOTAL
		STORE_ID
		STORE_NAME
    PRODUCT_LIST {
      PRODUCT_ID
      PRODUCT_NAME
      UNIT_PRICE
    }
		_id
  }
}
```

```JSON
{
  "data": {
    "ngPosCustomerOrders": [
      {
        "CUSTOMER_ID": "139",
        "EMAIL_ADDRESS": "elaine.moncure@internalmail",
        "FULL_NAME": "Elaine Moncure",
        "ORDER_DATETIME": "2023-04-06T11:05:56Z",
        "ORDER_STATUS": "COMPLETE",
        "ORDER_TOTAL": 52.92,
        "PRODUCT_LIST": [
          {
            "PRODUCT_ID": "19",
            "PRODUCT_NAME": "Men's Coat (Red)",
            "UNIT_PRICE": 28.21
          },
          {
            "PRODUCT_ID": "28",
            "PRODUCT_NAME": "Men's Hoodie (Red)",
            "UNIT_PRICE": 24.71
          }
        ],
        "STORE_ID": "3",
        "STORE_NAME": "Seattle",
        "_id": "64398a780c4e4d07cf6eacb6"
      },
      {
        "CUSTOMER_ID": "146",
        "EMAIL_ADDRESS": "rey.wada@internalmail",
        "FULL_NAME": "Rey Wada",
        "ORDER_DATETIME": "2023-04-06T11:05:56Z",
        "ORDER_STATUS": "COMPLETE",
        "ORDER_TOTAL": 82.41,
        "PRODUCT_LIST": [
          {
            "PRODUCT_ID": "19",
            "PRODUCT_NAME": "Men's Coat (Red)",
            "UNIT_PRICE": 28.21
          },
          {
            "PRODUCT_ID": "28",
            "PRODUCT_NAME": "Men's Hoodie (Red)",
            "UNIT_PRICE": 24.71
          },
          {
            "PRODUCT_ID": "9",
            "PRODUCT_NAME": "Women's Jeans (Brown)",
            "UNIT_PRICE": 29.49
          }
        ],
        "STORE_ID": "4",
        "STORE_NAME": "New York City",
        "_id": "6439fe117ec419fd7f5e88a8"
      }
    ]
  }
}
```

[https://us-west-2.aws.realm.mongodb.com/api/client/v2.0/app/nextgenpos-ooetv/graphql](https://us-west-2.aws.realm.mongodb.com/api/client/v2.0/app/nextgenpos-ooetv/graphql).  
[https://learning.postman.com/docs/sending-requests/authorization/#jwt-bearer](https://learning.postman.com/docs/sending-requests/authorization/#jwt-bearer)

### Query Curl Command
```
curl -X POST 'https://us-west-2.aws.realm.mongodb.com/api/client/v2.0/app/<APP-ID>/graphql' \
   --header 'email: <EMAIL ADRRESS>' \
   --header 'password: <PASSWORD>' \
   --header 'Content-Type: application/json' \
   --data-raw '{"query": "query {ngPosCustomerOrders(query:{CUSTOMER_ID:\"139\"}) {CUSTOMER_ID EMAIL_ADDRESS FULL_NAME ORDER_DATETIME ORDER_STATUS ORDER_TOTAL STORE_ID STORE_NAME PRODUCT_LIST { PRODUCT_ID PRODUCT_NAME UNIT_PRICE } _id}}"}'
```
### Insert one order Postman - Has to be a POST and not a GET... to pass in the graphQL mutation
```
mutation {
  insertOneNgPosCustomerOrder(data: {
    CUSTOMER_ID: "149"
    EMAIL_ADDRESS: "quinn.yerdon@internalmail"
    FULL_NAME: "Quinn Yerdon"
    ORDER_DATETIME: "2023-04-06T11:05:56Z"
    ORDER_STATUS: "COMPLETE"
    ORDER_TOTAL: 90.39
    STORE_ID: "16"
    STORE_NAME: "Sydney"
    PRODUCT_LIST: [
    	{ 
      PRODUCT_ID: "1"
      PRODUCT_NAME: "Boy's Shirt (White)"
      UNIT_PRICE: 29.55
      },
      { 
      PRODUCT_ID: "2"
      PRODUCT_NAME: "Women's Shirt (Green)"
      UNIT_PRICE: 16.17
      },
      { 
      PRODUCT_ID: "3"
      PRODUCT_NAME: "Boy's Sweater (Green)"
      UNIT_PRICE: 44.17
      }
  	]
  }) {
    _id
    CUSTOMER_ID
    EMAIL_ADDRESS
    FULL_NAME
    ORDER_DATETIME
    ORDER_STATUS
    ORDER_TOTAL
    STORE_ID
    STORE_NAME
    PRODUCT_LIST {
      PRODUCT_ID
      PRODUCT_NAME
      UNIT_PRICE
    }
  }
}
```

### Update CURL Command
```
curl -X POST 'https://us-west-2.aws.realm.mongodb.com/api/client/v2.0/app/<APP-ID>/graphql' \
   --header 'email: <EMAIL ADDRESS>' \
   --header 'password: <PASSWORD>' \
   --header 'Content-Type: application/json' \
   --data-raw '{"query": "mutation {updateOneNgPosCustomerOrder(query: { _id: \"643b362c63c60655d90b1159\" } set: { ORDER_TOTAL: 19.98 } ) { _id ORDER_TOTAL }}"}'
```

### Update Postman -- has to be a POST not a GET
```
mutation {
    updateOneNgPosCustomerOrder(
        query: { _id: "643b362c63c60655d90b1159" } 
        set: { 
            ORDER_TOTAL: 46.22, 
            PRODUCT_LIST: [
                { 
                PRODUCT_ID: "1"
                PRODUCT_NAME: "Boy's Shirt (White)"
                UNIT_PRICE: 29.55
                },
                { 
                PRODUCT_ID: "2"
                PRODUCT_NAME: "Women's Shirt (Green)"
                UNIT_PRICE: 16.17
                }
            ] 
            } ) 
        { 
        _id 
        CUSTOMER_ID
        ORDER_TOTAL 
        PRODUCT_LIST {
            PRODUCT_ID
            PRODUCT_NAME
            UNIT_PRICE
        }
        }
}
```

Store the document as binary data to be sent to Oracle as a blob.   
[https://www.mongodb.com/docs/manual/reference/method/BinData/](https://www.mongodb.com/docs/manual/reference/method/BinData/).   




# Updating Oracle

Oracle stores its product details information in the table as a BLOB.   

```json
{
  "colour" : "red",
  "gender" : "Girl's",
  "brand" : "BRANDNAME",
  "description" : "description",
  "sizes" : [ 
    "1 Yr", "2 Yr", "3-4 Yr", "5-6 Yr", "7-8 Yr", "9-10 Yr" 
  ],
  "reviews" :  [
    {
      "rating" : 9,
      "review" : "Review text"
    }
  ]
}
```

Exrtacting the data from the json document stored as a BLOB:

```SQL
select p.product_name, r.rating, 
       round ( 
         avg ( r.rating ) over (
           partition by product_name
         ),
         2
       ) avg_rating,
       r.review
from   products p,
       json_table (
         p.product_details, '$'
         columns ( 
           nested path '$.reviews[*]'
           columns (
             rating integer path '$.rating',
             review varchar2(4000) path '$.review'
           )
         )
       ) r;
```
