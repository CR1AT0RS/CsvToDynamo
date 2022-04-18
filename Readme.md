Simplified Python script to upload data from CSV to Dynamo DB. In this example we are using basic Email, Password example for key value store.

Packages required:
import sys
import csv
import boto3

```
Python3 is recommended:
import sys
import csv
import boto3

dynamodb = boto3.resource('dynamodb')

tableName = 'testing' # FIXME
filename = 'test.csv' # FIXME

def main():
    csvfile = open(filename)

    write_to_dynamo(csv.reader(csvfile, delimiter=','))

    return print("Done")

def write_to_dynamo(rows):
    table = dynamodb.Table(tableName)
    with table.batch_writer() as batch:
        for row in rows:
            # print(row)
            batch.put_item(
                Item={
                    'Email': row[0],
                    'Password': row[1] 
                }
            )

main()

```
