# AWS: Athena

> Reference: https://docs.aws.amazon.com/cli/latest/reference/athena/

## Execute A Query

The query will be executed in the background.

```sh
aws athena start-query-execution \
  --work-group <WORK_GROUP_NAME> \
  --query-execution-context Database=<DATABASE_NAME> \
  --query-string <QUERY>
```

Example Response

```
{
    "QueryExecutionId": "8f54de09-e59d-4ef1-b738-af6ebc849f84"
}
```

The `QueryExecutionId` will be used to retrieve the query status and query results.

## Retrieve the Query Status

```sh
aws athena get-query-execution --query-execution-id <QUERY_EXECUTION_ID>
```

## Retrieve the Query Results

```sh
aws athena get-query-results --query-execution-id <QUERY_EXECUTION_ID>
```

- You can "stream" the output by setting the `--page-size <N>` argument.
- Or, you can paginate the results by setting the `--max-items <N>` and the `--starting-token <NEXT_TOKEN>` arguments,
  where the `<NEXT_TOKEN>` is obtained from the last `get-query-results` call.

## Prepared Statement

### Create the Prepared Statement

```sh
aws athena create-prepared-statement \
  --work-group <WORK_GROUP_NAME> \
  --statement-name <STATEMENT_NAME> \
  --query-statement <QUERY>

# For example:
# aws athena create-prepared-statement \
#   --work-group primary \
#   --statement-name example \
#   --query-statement "SELECT * FROM demo WHERE created_at > CAST(? AS date) LIMIT 10"
```

### Execute the Prepared Statement

The prepared statement can be triggered by executing the `EXECUTE` query.

```sh
# For example:
# aws athena start-query-execution \
#   --work-group primary \
#   --query-execution-context Database=foo \
#   --query-string "EXECUTE example USING '2020-01-01'"
```

### Retrieve the Prepared Statement

```sh
aws athena get-prepared-statement --work-group <WORK_GROUP_NAME> --statement-name <STATEMENT_NAME>
```

### List the Prepared Statements

```sh
aws athena list-prepared-statements --work-group <WORK_GROUP_NAME>
```
