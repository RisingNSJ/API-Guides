# Personal Device Integration API

## Overview
The Personal Device Integration API enables employees to securely register and integrate their personal laptops with approved company platforms. This API helps validate device compatibility, enforce security requirements, and ensure authorized access during workforce transitions.

---
## Header Parameters
The table below lists the header parameters for the Personal Device Integration API. These parameters control authentication, request formatting, and request tracking.

| Parameter | Type | Required | Description |
|-|-|-|-
| Authorization | string | Yes | Enables the API to authenticate the request using a valid access token. |
| Content-Type | string | Yes | Specifies the format of the request body, typically `application/json`.|
| X-Request-ID | string | No | Helps track the request across systems for debugging and auditing.|
| Device-OS | string | No | Identifies the operating system running on the employee’s device. |
| Client-Version | string | No | Indicates the version of the client application making the request. |

---

## Request Parameters
The table below lists the input fields required to register and validate a personal device for platform access. These parameters help the API verify device ownership, compatibility, and security posture.

| Parameter | Type | Required | Description |
|-|-|-|-
| employeeID | string | Yes | Identifies the employee requesting device integration. |
| deviceID | string  | Yes | Uniquely identifies the personal laptop or device being registered. |
| operatingSystem | string | Yes | Specifies the operating system installed on the device. |
| osVersion | string | No | Indicates the version of the operating system. |
| securityCheck | boolean | Yes | Confirms whether required security checks are completed on the device. |
| purpose | string  | No | Describes the reason for requesting device access (for example, job search).|

## Error Codes
The table below lists common error codes returned by the Personal Device Integration API and explains how to resolve them.
| Code | Type | Description |
|-|-|-|
| 400 | Client | Bad request. Required parameters are missing or invalid. |
| 401 | Client | Unauthorized. The authorization token is missing or expired.|
| 403 | Client | Forbidden. The employee is not allowed to register a personal device. |
| 409 | Client | Conflict. The device is already registered for this employee. |
| 422 | Client | Validation error. The device does not meet security requirements. |
| 500 | Server | Internal server error occurred while processing the request. |
| 503 | Server | Service unavailable. Retry the request later. |

## Request Input
The Personal Device Integration API requires the following JSON input to register and validate a personal device for platform access.

```json
{
  "employeeID": "emp78945",
  "deviceID": "laptop-abc123",
  "operatingSystem": "macOS",
  "osVersion": "14.2",
  "securityCheck": true,
  "purpose": "Apply for internal roles"
}
```
### Description of Fields

| Field | Type | Required | Description |
|-|-|-|-|
| employeeID | string | Yes | Identifies the employee requesting device integration. |
| deviceID | string | Yes | Uniquely identifies the personal device that the employee is registering. |
| operatingSystem | string  | Yes | Specifies the operating system installed on the device. |
| osVersion | string  | No | Indicates the version of the operating system. |
| securityCheck | boolean | Yes | Confirms required security checks are completed. |
| purpose | string | No | Explains why access is being requested. |

## Response Output
The Personal Device Integration API returns the following JSON response after validating and processing the device integration request.

```json
{
  "integrationStatus": "Approved",
  "deviceID": "laptop-abc123",
  "accessGranted": true,
  "validationMessage": "Device meets all security requirements.",
  "approvedPlatforms": [
    "Internal Job Portal",
    "Learning Management System",
    "Career Transition Tools"
  ],
  "timestamp": "2026-01-30T10:45:00Z"
}
```
### Description of Fields

| Field | Type | Description |
|-|-|-|
| integrationStatus | string | Indicates the final status of the device integration request.|
| deviceID | string | Confirms the ID of the registered personal device.|
| accessGranted | boolean | Shows whether platform access was granted.|
| validationMessage | string  | Explains the result of the security validation. |
| approvedPlatforms | array | Lists the platforms the device can access.|
| timestamp | string | Indicates when the API processed the request. |

