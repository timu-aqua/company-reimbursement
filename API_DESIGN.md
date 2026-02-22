# API Design Documentation

## Overview
This document provides comprehensive documentation for the API endpoints of the Company Reimbursement system.

## Authentication
- **Endpoint:** `/api/auth/login`
- **Method:** POST
- **Request Body:**  
  ```json
  {
    "username": "user@example.com",
    "password": "yourpassword"
  }
  ```
- **Response:**  
  - **200 OK:**  
    ```json
    {
      "token": "your.jwt.token",
      "expiresIn": 3600
    }
    ```  
  - **401 Unauthorized:**  
    ```json
    {
      "error": "Invalid credentials"
    }
    ```

## Reimbursement Requests
- **Endpoint:** `/api/reimbursements`
- **Method:** POST
- **Request Body:**  
  ```json
  {
    "amount": 100,
    "category_id": 1,
    "description": "Office supplies"
  }
  ```
- **Response:**  
  - **201 Created:**  
    ```json
    {
      "id": 1,
      "amount": 100,
      "status": "pending"
    }
    ```  
  - **400 Bad Request:**  
    ```json
    {
      "error": "Invalid request data"
    }
    ```

## Document Uploads
- **Endpoint:** `/api/reimbursements/{id}/documents`
- **Method:** POST
- **Request Body:**  
  ```json
  {
    "file": "binary data"
  }
  ```
- **Response:**  
  - **200 OK:**  
    ```json
    {
      "message": "File uploaded successfully"
    }
    ```  
  - **404 Not Found:**  
    ```json
    {
      "error": "Reimbursement not found"
    }
    ```

## Reviews
- **Endpoint:** `/api/reimbursements/{id}/reviews`
- **Method:** POST
- **Request Body:**  
  ```json
  {
    "rating": 5,
    "comment": "Great service!"
  }
  ```
- **Response:**  
  - **201 Created:**  
    ```json
    {
      "id": 10,
      "rating": 5,
      "comment": "Great service!"
    }
    ```  
  - **400 Bad Request:**  
    ```json
    {
      "error": "Invalid review data"
    }
    ```

## Reports
- **Endpoint:** `/api/reports`
- **Method:** GET
- **Query Parameters:**  
  - `fromDate`: (string) Start date of report.
  - `toDate`: (string) End date of report.
- **Response:**  
  - **200 OK:**  
    ```json
    [
      {
        "id": 1,
        "total": 1000
      }
    ]
    ```  
  - **400 Bad Request:**  
    ```json
    {
      "error": "Invalid date range"
    }
    ```

## Categories
- **Endpoint:** `/api/categories`
- **Method:** GET
- **Response:**  
  - **200 OK:**  
    ```json
    [
      {
        "id": 1,
        "name": "Office Supplies"
      }
    ]
    ```  

## Error Handling
All endpoints respond with standardized error responses containing an error message and applicable error code.