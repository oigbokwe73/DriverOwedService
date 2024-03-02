# Ride Matching Service Documentation

## Overview

The Ride Matching Service connects riders with drivers, facilitating quick and efficient ride arrangements. This document outlines the service's functionality, including API endpoints, request/response formats, and examples.

## Features

- **Ride Requests**: Riders can request rides, specifying pickup and dropoff locations.
- **Driver Matching**: The service matches ride requests with available drivers based on location and other criteria.
- **Ride Status Updates**: Both riders and drivers can receive updates on ride status, including match confirmation, ride progress, and completion.
- **Ratings and Feedback**: After ride completion, riders and drivers can rate each other and provide feedback.

## API Endpoints

### Request a Ride

- **POST** `/api/ride-requests`

  Allows a rider to request a ride.

  #### Request Body

  ```json
  {
    "riderId": 1,
    "pickupLocation": "123 Main St, Anytown, AN",
    "dropoffLocation": "456 Elm St, Anytown, AN"
  }
  ```

  #### Response

  ```json
  {
    "requestId": 101,
    "status": "pending",
    "requestTime": "2024-03-01T12:34:56Z"
  }
  ```

### Update Driver Status

- **POST** `/api/drivers/{driverId}`

  Updates the current status of a driver.

  #### Request Body

  ```json
  {
    "currentLocation": "789 Oak St, Anytown, AN",
    "status": "available"
  }
  ```

  #### Response

  ```json
  {
    "driverId": 5,
    "lastUpdated": "2024-03-01T12:40:00Z"
  }
  ```

### Get Ride Match

- **GET** `/api/ride-matches/{requestId}`

  Retrieves the match details for a specific ride request.

  #### Response

  ```json
  {
    "matchId": 202,
    "requestId": 101,
    "driverId": 5,
    "matchTime": "2024-03-01T12:45:00Z",
    "status": "accepted"
  }
  ```

## Data Models

### Ride Request

- `requestId`: Integer
- `riderId`: Integer
- `pickupLocation`: String
- `dropoffLocation`: String
- `requestTime`: DateTime
- `status`: String (pending, matched, cancelled, completed)

### Driver Status

- `driverId`: Integer
- `currentLocation`: String
- `status`: String (available, on_trip, offline)
- `lastUpdated`: DateTime

### Ride Match

- `matchId`: Integer
- `requestId`: Integer
- `driverId`: Integer
- `matchTime`: DateTime
- `status`: String (accepted, driver_en_route, in_progress, completed, cancelled)

## Additional Information

- **Authentication**: All API requests require an API key or user authentication token.
- **Rate Limiting**: API requests are limited to 1000 requests per hour per user to ensure service reliability.
- **Error Handling**: The service uses standard HTTP response codes to indicate the success or failure of API requests.

For more detailed information on request parameters, response objects, and error codes, please refer to the full API documentation.

---

This Markdown template provides a basic structure for documenting a Ride Matching Service. You can expand each section with more details specific to your service, including authentication methods, detailed request/response models, and any additional endpoints or features not covered here.
