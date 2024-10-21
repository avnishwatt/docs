# PE-Validator API Documentation

This document provides information on how to consume the PE-Validator API.

## Base URL

```
It will be provided to you by our team

```

Replace this with your actual base URL.

## Authentication

All API requests require authentication. Include your API key in the header of each request:

```
Authorization: Bearer YOUR_API_KEY
```

## Endpoints

### 1. Analyze Solar Panel Installation

Analyzes solar panel installation images from a PDF or ZIP file.

- **URL**: `/api/analyze`
- **Method**: `POST`
- **Content-Type**: `multipart/form-data`

#### Request Parameters

| Parameter | Type   | Required | Description                               |
|-----------|--------|----------|-------------------------------------------|
| file      | File   | Yes      | PDF or ZIP file containing images         |
| userId    | String | Yes      | Unique identifier for the user            |

#### Response

```json
{
  "finalReport": {
    "solarPanelPhotos": {
      "total": "5"
    },
    "sufficientPanelPhotos": "Yes",
    "workmanshipAcceptable": "Yes",
    "solarPanelNameplatePresent": "Yes",
    "solarPanelsPresent": "Yes",
    "solarPanelBrand": "SunPower",
    "batteryPresent": "No",
    "batteryPhotos": {
      "total": "0",
      "closeUp": "0",
      "farAway": "0"
    },
    "batteryPhotosComplete": "N/A",
    "batteryBrand": "N/A",
    "mountingSystem": {
      "type": "Roof mount"
    },
    "inverterPresent": "Yes",
    "inverterDetails": {
      "brand": "SolarEdge",
      "model": "SE7600H-US"
    }
  }
}
```

#### Error Responses

- `400 Bad Request`: Invalid input or missing required fields
- `413 Payload Too Large`: File size exceeds the maximum limit
- `422 Unprocessable Entity`: Unable to process the uploaded file
- `500 Internal Server Error`: Server-side error

### 2. Chat About Solar Panel Installation

Allows users to ask questions about their analyzed solar panel installation.

- **URL**: `/api/chat`
- **Method**: `POST`
- **Content-Type**: `application/json`

#### Request Body

```json
{
  "userId": "user123",
  "message": "How many solar panel photos were included?"
}
```

#### Response

```json
{
  "response": "Based on the analysis, there were a total of 5 solar panel photos included in the submission."
}
```

#### Error Responses

- `400 Bad Request`: Invalid input or missing required fields
- `500 Internal Server Error`: Server-side error

## Rate Limiting

The API is rate-limited to 100 requests per 15-minute window per IP address.

## File Size Limits

- Maximum file size: 50MB

## Best Practices

1. Always check the response status code and handle errors appropriately.
2. Implement exponential backoff for retries in case of server errors.
3. Store the `userId` securely on your end, as it's required for both analyze and chat endpoints.
4. For the analyze endpoint, consider implementing a progress indicator on your frontend, as processing may take some time.

## Support

For any issues or questions, please contact our support team.