# Realtime Transaction Statistics

## Coding challenge from the world's first Mobile Bank based out of Berlin, Germany.

The main use case for the API is to calculate realtime statistics for the last 60 seconds of transactions.

The API needs the following endpoints:

    POST /transactions – called every time a transaction is made. It is also the sole input of this rest API.
    GET /statistics – returns the statistic based of the transactions of the last 60 seconds.
    DELETE /transactions – deletes all transactions.
 
Specs

POST /transactions

This endpoint is called to create a new transaction.

Body:

{
  "amount": "12.3343",
  "timestamp": "2018-07-17T09:59:51.312Z"
}

Where:

    amount – transaction amount; a string of arbitrary length that is parsable as a BigDecimal
    timestamp – transaction time in the ISO 8601 format YYYY-MM-DDThh:mm:ss.sssZ in the UTC timezone (this is not the current timestamp)

Returns: Empty body with one of the following:

    201 – in case of success
    204 – if the transaction is older than 60 seconds
    400 – if the JSON is invalid
    422 – if any of the fields are not parsable or the transaction date is in the future

GET /statistics

This endpoint returns the statistics based on the transactions that happened in the last 60 seconds. It must execute in constant time and memory (O(1)).

Returns:

{
  "sum": "1000.00",
  "avg": "100.53",
  "max": "200000.49",
  "min": "50.23",
  "count": 10
}
 
Where:

    sum – a BigDecimal specifying the total sum of transaction value in the last 60 seconds
    avg – a BigDecimal specifying the average amount of transaction value in the last 60 seconds
    max – a BigDecimal specifying single highest transaction value in the last 60 seconds
    min – a BigDecimal specifying single lowest transaction value in the last 60 seconds
    count – a long specifying the total number of transactions that happened in the last 60 seconds

All BigDecimal values always contain exactly two decimal places and use `HALF_ROUND_UP` rounding. eg: 10.345 is returned as 10.35 10.8 is returned as 10.80

DELETE /transactions

This endpoint causes all existing transactions to be deleted
The endpoint should accept an empty request body and return a 204 status code.

Requirements

For the Rest API, the most important and maybe most challenging requirement is to make GET /statistics execute in constant time and memory. Note, however, that this is not the only requirement so it is strongly recommended to tackle this last.

These are the additional requirements for the solution:

    Free to choose any JVM language to complete the challenge in, but the application has to be run in Maven.

    The API has to be threadsafe with concurrent requests.

    The solution has to work without a database (this also applies to in-memory databases).

    Unit tests are mandatory.

    mvn clean install and mvn clean integration-test must complete successfully.

    Please ensure that no changes are made to the src/it folder since automated tests will be run against the solution.

