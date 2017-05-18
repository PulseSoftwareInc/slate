# V2 Resources

## Real-time Feedback

Real-time Feedback represents an instance of feedback that was given from a sender to a recipient, with
text content created by the sender. The V2 version of this endpoint provides support for Team Recognition, or Real-time
Feedback with multiple recipients.

### Attributes

Item        | Description
----        | -----------
uuid        | A unique identifier associated with this feedback
sender      | An Employee object, the person who gave the feedback
recipients  | An array of Employee objects, the people who received the feedback
content     | The publicly visible content of the feedback
created_at  | The time the feedback was created and sent

### Endpoints

```shell
curl "https://api.reflektive.com/v2/real-time-feedback?created_after=1477877614"
  -H "Authorization: Token token=authentication_token"
```

> Sample JSON Response

```json
{
  "links": {
    "self": "/v2/real-time-feedback?created_after=1477877614"
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
      "recipients": [
        {
          "uuid": "addd9666-788a-4eb6-82a2-225a7600e4c9",
          "email": "luke.skywalker@example.com",
          "name": "Luke Skywalker",
          "photo": "https://www.example.com/luke.skywalker.jpg"
        }
      ],
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
      "recipients": [
        {
          "uuid": "962e6d3a-ade5-4bc7-8672-70236075be5a",
          "email": "han.solo@example.com",
          "name": "Han Solo",
          "photo": "https://www.example.com/han.solo.jpg"
        },
        {
          "uuid": "e4f3d7e4-47c1-4dfc-8dc5-0b05f625840b",
          "email": "rey@example.com",
          "name": "Rey",
          "photo": "https://www.example.com/rey.jpg"
        },
        {
          "uuid": "fff3d7e4-4bc1-4efc-adc5-0b05f953840f",
          "email": "b.b.8@example.com",
          "name": "BB-8",
          "photo": "https://www.example.com/bb8.jpg"
        }
      ],
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
      "self": "/v2/real-time-feedback?created_after=1477877614",
      "next": "/v2/real-time-feedback?created_after=1477877614?page=2",
      "last": "/v2/real-time-feedback?created_after=1477877614?page=5"
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
      "recipients": [
        {
          "uuid": "addd9666-788a-4eb6-82a2-225a7600e4c9",
          "email": "luke.skywalker@example.com",
          "name": "Luke Skywalker",
          "photo": "https://www.example.com/luke.skywalker.jpg"
        }
      ],
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
      "recipients": [
        {
          "uuid": "962e6d3a-ade5-4bc7-8672-70236075be5a",
          "email": "han.solo@example.com",
          "name": "Han Solo",
          "photo": "https://www.example.com/han.solo.jpg"
        },
        {
          "uuid": "e4f3d7e4-47c1-4dfc-8dc5-0b05f625840b",
          "email": "rey@example.com",
          "name": "Rey",
          "photo": "https://www.example.com/rey.jpg"
        },
        {
          "uuid": "fff3d7e4-4bc1-4efc-adc5-0b05f953840f",
          "email": "b.b.8@example.com",
          "name": "BB-8",
          "photo": "https://www.example.com/bb8.jpg"
        }
      ],
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

`GET https://api.reflektive.com/v2/real-time-feedback`

### Query Parameters

Parameter       | Default                                        | Description
---------       | -------                                        | -----------
created_before  | Time the request was issued                    | A UNIX timestamp representing the oldest time a feedback was created
created_after   | 1 day prior to the time the request was issued | UNIX timestamp representing the most recent time a feedback was created
page            | 1                                              | An offset for the feedback results. The endpoint will return 200 results per query
