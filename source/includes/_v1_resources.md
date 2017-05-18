# V1 Resources

## Employee

An Employee is an object that represents a user working for a Reflektive company.

### Attributes

Item        | Description
----        | -----------
uuid        | A unique identifier associated with this employee
email       | The email address of the employee
name        | The employee's full name, for example: "John Smith"
photo       | A URL pointing to a photograph of the employee (if one is available)

## Real-time Feedback

Real-time Feedback represents an instance of feedback that was given from a sender to a recipient, with
text content created by the sender.

### Attributes

Item        | Description
----        | -----------
uuid        | A unique identifier associated with this feedback
sender      | An Employee object, the person who gave the feedback
recipient   | An Employee object, the person who received the feedback
content     | The publicly visible content of the feedback
created_at  | The time the feedback was created and sent

### Endpoints

```shell
curl "https://api.reflektive.com/v1/real-time-feedback?created_after=1477877614"
  -H "Authorization: Token token=authentication_token"
```

> Sample JSON Response

```json
{
  "links": {
    "self": "/v1/real-time-feedback?created_after=1477877614"
  },
  "data": [
    {
      "uuid": "e8678ff9-3ae4-4b2b-b7af-f7240155f753",
      "sender": {
        "uuid": "04b09952-6b79-454e-8306-9c7f015267b5",
        "email": "darth.vader@example.com",
        "name": "Darth Vader",
        "photo": "https://www.example.com/darth.vader.jpg"
      },
      "recipient": {
        "uuid": "addd9666-788a-4eb6-82a2-225a7600e4c9",
        "email": "luke.skywalker@example.com",
        "name": "Luke Skywalker",
        "photo": "https://www.example.com/luke.skywalker.jpg"
      },
      "content": "Most impressive.",
      "created_at": "2016-10-31T23:43:20Z"
    },
    {
      "uuid": "ab5eea44-bfd6-4e16-8129-12963efd054b",
      "sender": {
        "uuid": "4dd3d0f0-d856-4981-b376-5602c07cad4f",
        "email": "chewbacca@example.com",
        "name": "Chewbacca",
        "photo": "https://www.example.com/chewbacca.jpg"
      },
      "recipient": {
        "uuid": "962e6d3a-ade5-4bc7-8672-70236075be5a",
        "email": "han.solo@example.com",
        "name": "Han Solo",
        "photo": "https://www.example.com/han.solo.jpg"
      },
      "content": "Raawwrr",
      "created_at": "2016-10-31T23:22:28Z"
    }
  ]
}
```
> Sample Paginated JSON Response

```json
{
  "links": {
      "self": "/v1/real-time-feedback?created_after=1477877614",
      "next": "/v1/real-time-feedback?created_after=1477877614?page=2",
      "last": "/v1/real-time-feedback?created_after=1477877614?page=5"
  },
  "data": [
    {
      "uuid": "e8678ff9-3ae4-4b2b-b7af-f7240155f753",
      "sender": {
        "uuid": "04b09952-6b79-454e-8306-9c7f015267b5",
        "email": "darth.vader@example.com",
        "name": "Darth Vader",
        "photo": "https://www.example.com/darth.vader.jpg"
      },
      "recipient": {
        "uuid": "addd9666-788a-4eb6-82a2-225a7600e4c9",
        "email": "luke.skywalker@example.com",
        "name": "Luke Skywalker",
        "photo": "https://www.example.com/luke.skywalker.jpg"
      },
      "content": "Most impressive.",
      "created_at": "2016-10-31T23:43:20Z"
    },
    {
      "uuid": "ab5eea44-bfd6-4e16-8129-12963efd054b",
      "sender": {
        "uuid": "4dd3d0f0-d856-4981-b376-5602c07cad4f",
        "email": "chewbacca@example.com",
        "name": "Chewbacca",
        "photo": "https://www.example.com/chewbacca.jpg"
      },
      "recipient": {
        "uuid": "962e6d3a-ade5-4bc7-8672-70236075be5a",
        "email": "han.solo@example.com",
        "name": "Han Solo",
        "photo": "https://www.example.com/han.solo.jpg"
      },
      "content": "Raawwrr",
      "created_at": "2016-10-31T23:22:28Z"
    }
  ]
}
```

### List all public, positive feedback

By default, results are paginated with 200 results per query. If your request returns more than 200 results,
links with page numbers directing to the next and last pages of results will be provided in the JSON response.

### Endpoint

`GET https://api.reflektive.com/v1/real-time-feedback`

### Query Parameters

Parameter       | Default                                        | Description
---------       | -------                                        | -----------
created_before  | Time the request was issued                    | A UNIX timestamp representing the oldest time a feedback was created
created_after   | 1 day prior to the time the request was issued | UNIX timestamp representing the most recent time a feedback was created
page            | 1                                              | An offset for the feedback results. The endpoint will return 200 results per query

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


