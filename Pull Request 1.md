
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
- `location`: The location of the event (optional).
- `description`: The description of the event (optional).
- `calendar_link`: The calendar link for the event (optional).
- `instagram_link`: The Instagram link for the event (optional).

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


## eventUpdate

API Endpoint: `/api/v1/event/:id/update`

Description: Update an existing event.

Method: PUT

Parameters:

- `id` (required): The ID of the event to update.
- `title`: The updated title of the event (optional).
- `status`: The updated status of the event (optional).
- `start_time`: The updated start time of the event (optional).
- `end_time`: The updated end time of the event (optional).
- `location`: The updated location of the event (optional).
- `description`: The updated description of the event (optional).
- `calendar_link`: The updated calendar link for the event (optional).
- `instagram_link`: The updated Instagram link for the event (optional).

Request URL Example: `http://127.0.0.1:5000/api/v1/event/123/update`

Request Method: PUT

Request Body Example:

```json
{
	  "title": "Updated Event Title",
	  "status": "updated",
	  "start_time": "2023-05-20T11:00:00",
	  "end_time": "2023-05-20T15:00:00",
	  "location": "Updated Event Location",
	  "description": "Updated Event Description",
	  "calendar_link": "https://example.com/updated-calendar",
	  "instagram_link": "https://www.instagram.com/updated-event"
}
```

Response Format: JSON

Response Example:

```json
{
	"message": "Successful"
}
```

```json
{
    "message": "Event not found"
}
```

```json
{
    "message": "Failed",
    "errors": [
        {
            "type": "field",
            "value": "Upcoming",
            "msg": "Status must be either upcoming or past.",
            "path": "status",
            "location": "body"
        }
    ]
}
```


## eventDelete

API Endpoint: `/api/v1/event/:id/delete`

Description: Delete an event.

Method: DELETE

Parameters:

- `id` (required): The ID of the event to delete.

Request URL Example: `http://127.0.0.1:5000/api/v1/event/123/delete`

Request Method: DELETE

Response Format: JSON

Response Example:

```json

```

```json
{
    "message": "Event not found"
}
```