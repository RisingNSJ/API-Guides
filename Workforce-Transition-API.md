# Workforce Transition API

## Overview
The Workforce Transition API enables you to fetch information about employees impacted in workforce changes, including departments, employee IDs, and communication details. This API helps HR teams, managers, and internal applications track workforce transitions efficiently.

## Header Parameters
The table below lists the header parameters for the Workforce Transition API. Each parameter enables you to control how the API processes your request and returns the response.

| Parameter | Type | Required | Description |
|-|-|-|-|
| Authorization | string | Yes | Enables the API to verify your identity and authorize your request using a token. |
| Content-Type  | string | Yes  | Tells the API the format of your request body, typically `application/json`. |
| X-Request-ID | string | No | Tracks your request by providing a unique ID for troubleshooting and correlation.|
| Accept-Language | string | No | Lets the API return messages in your preferred language. |
| Client-Version | string | No | Communicates which version of the client application is making the request. |

## Request Parameters
The table below lists the input fields for the Workforce Transition API request. Each field enables the API to fetch and return information about impacted employees accurately.

| Parameter | Type | Required | Description |
|-|-|-|-|
| department | string | Yes | Enables the API to filter employees by their department. |
| employeeAlias | string | No | Lets the API fetch employee information using their alias. |
| employeeID | string | No | Enables the API to return details for a specific employee. |
| includeContact | boolean | No | Lets the API include contact and communication details in the response. |

## Response Parameters
The table below lists the response parameters returned by the Workforce Transition API, describing each field, its data type, and its purpose.

| Parameter | Type | Description |
|-|-|-|
| employees | array | Contains the list of employees impacted in workforce changes. |
| employees.employeeID | string  | Specifies the unique ID assigned to each employee. |
| employees.alias | string  | Provides the employee’s system alias or username. |
| employees.department | string | Indicates the department to which the employee belongs. |
| employees.communication | string  | Shows the status of communication sent to the employee regarding workforce changes. |
| employees.manager | string  | Provides the name of the employee’s manager.|
| totalCount | integer | Shows the total number of employees returned in this API response. |

## Error Codes
The table below lists possible error codes and their meanings when calling the Workforce Transition API.

| Code | Type | Description |
|-|-|-|
| 400 | Client | Bad request. The request parameters are missing or invalid. |
| 401 | Client | Authorization token is missing or invalid. |
| 403 | Client | The client does not have permission to access this resource. |
| 404 | Client | No employees were found matching the request parameters.|
| 500  | Server | Internal server error. Something went wrong on the server while processing the request.|
| 503  | Server | Service unavailable. The API is temporarily unavailable, retry after some time. |

## Request Input
The Workforce Transition API requires the following JSON input in the request body. Use this structure to fetch details about employees impacted in workforce changes.

```json
{
    "department": "Engineering",
    "employeeAlias": "jdoe",
    "employeeID": "12345",
    "includeContact": true
}
```
### Description of Fields

| Field | Type | Required | Description |
|-|-|-|-|
| department | string | Yes | Filters employees by the specified department. |
| employeeAlias | string | No | Returns employee information using their alias. |
| employeeID | string | No | Returns details for a specific employee. |
| includeContact | boolean | No | If true, returns communication details sent to the employee. |

## Response Output
The Workforce Transition API returns the following JSON structure. It provides detailed information about employees impacted in workforce changes.

```json
{
    "employees": [
        {
            "employeeID": "12345",
            "alias": "jdoe",
            "department": "Engineering",
            "communication": "Email sent on 2026-01-30",
            "manager": "Jane Smith"
        },
        {
            "employeeID": "67890",
            "alias": "asmith",
            "department": "HR",
            "communication": "Email pending",
            "manager": "Robert Brown"
        }
    ],
    "totalCount": 2
}
```

### Description of Fields

| Field | Type | Description |
|-|-|-|
| employees | array | Contains the list of employees impacted in workforce changes. |
| employees.employeeID | string | Specifies the unique ID assigned to each employee. |
| employees.alias | string | Provides the employee’s system alias or username. |
| employees.department | string | Indicates the department to which the employee belongs. |
| employees.communication | string | Shows the status of communication sent to the employee regarding workforce changes. |
| employees.manager | string  | Provides the name of the employee’s manager. |
| totalCount | integer | Shows the total number of employees returned in this API response. |
