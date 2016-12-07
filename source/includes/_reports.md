## Report

Generate reports by submitting HTTP POST requests. These endpoints will kick off a report generation
and return the uuid of a Task in order to monitor the status of the report generation.
When the report generation has completed, the Task's status will be updated to "complete" and its metadata will be updated
to contain a link where the report can be accessed. This is a public link that will by default expire after 15 minutes.
Keep track of a Task's status using the `GET https://api.reflektive.com/v1/task/:uuid` endpoint

### Endpoints

```shell
curl -X POST "https://api.reflektive.com/v1/reports/reviews?report_type=calibrations&cycle_uuid=eadf6d0c-00e3-45ce-8332-1673226f0321"
    -H "Authorization: Token token=authentication_token"
```

> Sample JSON Response

```json
{
  "data": {
    "task_uuid": "194b434f-ebbb-4aae-a975-34681d13c1b3"
  }
}
```

### Calibrations Report

### Endpoint

`POST https://api.reflektive.com/v1/reports/reviews?report_type=calibrations&cycle_uuid=:uuid`


