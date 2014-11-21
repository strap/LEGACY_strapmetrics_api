#StrapMetrics API 
###v0.2.6 (November 2014)

##Getting Started

* You access a resource by sending an HTTP request to the StrapMetrics API. The server replies with a response that either contains the data you requested, or a status indicator, or both.
* All resources are located at https://api.straphq.com/
* You request a particular resource by appending a particular path to this base URL that specifies the resource.
* On this page, when a portion of a URL, path, or parameter value is shown in italics, this indicates that you should replace the italicized value with a particular value appropriate to your request.
* Unless otherwise noted, the response type is always JSON.

##Authentication

All API calls require a valid *app_id*. To get an app_id, create an app on the dashboard. Soon, some calls will require an additional *auth_token* 

##How to Use These Reference Entries

This page has reference entries for the various resources in the StrapMetrics  API. Each reference entry generally includes the following information:

* The resource path (the part of the URL that specifies the particular resource)
* A list of the allowed and required parameters and a description of their possible values
* A description of what the resource does
* The HTTP verbs you can use when accessing the resource
* The sorts of responses that the resource returns, and one or more response examples
* Any status codes that the StrapMetrics API might return that are specific to this resource

##Event Resources

Use the following POST request to log an event for your app. 

/create/event/with

###Parameters

Parameter | Description | Values
--- | --- | ---
**app_id** | App ID (Create one in the Strap Dashboard) | Any valid App ID
**visitor_id** | A unique identifier for this visitor/user. Pass additional user info in cvar. | Any valid unique Visitor ID string
visitor_timeoffset | Timezone offset from UTC in hours | ex: -5 
action_url | A URI style path to the event. | Any string is valid, but recommend format is "/category/event"
action_name | A friendly name for the action_url | Any string is valid, but recommended format is "Event Name"
lat | Latitude | Valid latitude in decimal degrees
lon | Longitude | Valid longitude in decimal degrees
accl | accelerometer measurements | Sent via encoded JSON, with ts in milliseconds ex: [ { ts: 1234567891000, x: -400, y: -400, z: -400 }, ... ]
cvar | Custom variables | Any valid JSON, useful for custom event data not captured elsewhere in API
activity | Activity user is performing | Defaults to UNKNOWN, used for providing activity algorithm with training data.
resolution | Device screen resolution, if applicable | ex: "144x168"
useragent | Device useragent | ex: "PEBBLE/2.3"

##Report Resources

Use the following GET requests to retrieve reports for your app. Currently all reports are returned with values totaled by day. Each report record contains totals for unique users, unique session counts, and total number of events.

/reports - get all available report endpoints. Returns an array of available reports.

* /reports/session - session counts
* /reports/hourly - totals by hour
* /reports/city - totals by city
* /reports/region - totals by region
* /reports/country - totals by country
* /reports/event - totals by event
* /reports/activity - totals by activity
* /reports/http_useragent - totals by http_useragent
* /reports/wearable_useragent - totals by wearable_useragent
* /reports/visitor - totals by visitor
* /reports/cvars - totals of custom variables


###Parameters

Parameter | Description | Values | Default
--- | --- | --- | ---
**token** | API Key (Create one in the Strap Dashboard) | A valid API Key |
**app_id** | App ID (Create one in the Strap Dashboard) | A valid App ID |
start_date | Start date to filter records from | Epoch timestamp in milliseconds | Today - 7 days
end_date | End date to filter records to | Epoch timestamp in milliseconds | Today


