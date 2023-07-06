
## eventList

API Endpoint: `/api/v1/events`

Description: Retrieve a list of events.

Method: GET

Parameters: None

Request URL Example: `http://127.0.0.1:5000/api/v1/events`

Response Format: JSON

Response Example:

```json
[
  {
    "_id": "123",
    "title": "Event 1",
    "status": "past",
    "start_time": "2023-05-20T10:00:00",
    "end_time": "2023-05-20T14:00:00",
    "location": "New York",
    "description": "Lorem ipsum",
    "calendar_link": "https://example.com/calendar",
    "instagram_link": "https://www.instagram.com/event1"
  },
  {
    "_id": "456",
    "title": "Event 2",
    "status": "upcoming",
    "start_time": "2023-06-10T18:00:00",
    "end_time": "2023-06-10T21:00:00",
    "location": "San Francisco",
    "description": "Dolor sit amet",
    "calendar_link": "https://example.com/calendar",
    "instagram_link": "https://www.instagram.com/event2"
  }
]
```


## eventDetail

API Endpoint: `/api/v1/event/:id`

Description: Retrieve details of the event with the specified ID.

Method: GET

Parameters:

- `:id` (URL parameter) - The ID of the event to retrieve.

Request URL Example: `http://127.0.0.1:5000/api/v1/event/123`

Response Format: JSON

Response Example:

```json
{
  "_id": "123",
  "title": "My Event",
  "status": "upcoming",
  "start_time": "2023-05-20T10:00:00",
  "end_time": "2023-05-20T14:00:00",
  "location": "New York",
  "description": "Lorem ipsum",
  "calendar_link": "https://example.com/calendar",
  "instagram_link": "https://www.instagram.com/myevent"
}
```


## eventCreate

API Endpoint: `/api/v1/event/create`

Description: Create a new event.

Method: POST

Parameters:

- `title`: The title of the event.
- `status`: The status of the event.
- `start_time`: The start time of the event.
- `end_time`: The end time of the event.
- `location`: (optional) The location of the event.
- `description`: (optional) The description of the event.
- `calendar_link`: (optional) The calendar link for the event.
- `instagram_link`: (optional) The Instagram link for the event.

Request URL Example: `http://127.0.0.1:5000/api/v1/event/creat`

Request Method: POST

Request Body Example:

```json
{
	"title": "Event Title",
	"status": "active",
	"start_time": "2023-05-20T10:00:00",
	"end_time": "2023-05-20T14:00:00",
	"location": "Event Location",
	"description": "Event Description",
	"calendar_link": "https://example.com/calendar",
	"instagram_link": "https://www.instagram.com/event"
}
```

Response Format: JSON

Response Examples:

```json
{
    "id": "123",
	"message": "Successful"
}
```

```json
{
    "message": "Failed",
    "errors": [
        {
            "type": "field",
            "value": "",
            "msg": "Status must be specified.",
            "path": "status",
            "location": "body"
        },
        {
            "type": "field",
            "value": "",
            "msg": "Status must be either upcoming or past.",
            "path": "status",
            "location": "body"
        }
    ]
}
```