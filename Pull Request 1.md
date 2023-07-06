
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
    "status": "active",
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
    "status": "active",
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

