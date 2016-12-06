## Task

Tasks keep track of the status of a particular job. For instance, Tasks are used to monitor the status
of report generations and are updated upon completion or failure of these report generation jobs.

### Attributes

Item       | Description
----       | -----------
uuid       | A unique identifier
status     | A string representing the status of this task (e.g. 'pending', 'failed', or 'completed')
metadata   | A JSON object containing metadata regarding this particular task

### Endpoints

```shell
curl "https://api.reflektive.com/v1/task/c4ff9ae5-558d-400c-a768-ad132a3e4c6c"
    -H "Authorization: Token token=authentication_token"
```

> Sample JSON Response

```json
{
  "data": {
    "uuid": "c4ff9ae5-558d-400c-a768-ad132a3e4c6c",
    "status": "pending",
    "metadata": {}
  }
}
```

```json
{
  "data": {
    "uuid": "c4ff9ae5-558d-400c-a768-ad132a3e4c6c",
    "status": "completed",
    "metadata": {
      "link": "http://www.some_download_link.com"
    }
  }
}
```

### Show the status of a given task

### Endpoint

`GET https://api.reflektive.com/v1/task/:uuid`