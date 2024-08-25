# Serverless Raffle App

This is a serverless raffle application using AWS serverless services. The app consists of two HTML pages and three AWS Lambda functions.

## Application Overview

1. **Apply Page**: 
   - Users submit their information on the "apply" page.
   - The "apply" function records this information in DynamoDB and adds an additional attribute `"win": "no"` to each record.

2. **Count Page**:
   - Displays the total number of people who have applied.
   - Calls the "count" function to retrieve the number of applicants from DynamoDB.
   - Includes a "Draw" button that, when clicked, calls the "draw" function.

3. **Draw Function**:
   - Randomly selects three entries in DynamoDB and changes their `"win"` attribute to `"yes"`.
   - The winners are then displayed on the "count" page.

## Architecture

![Architecture](Arceticture.png)

### How It Works

- **Domain Setup**:
  - The domain "ahmedsamy.link" is managed by Route 53.
  - Requests to "ahmedsamy.link" are redirected to CloudFront, which caches the HTML content.
  
- **Apply Page**:
  - When the user submits information on the "apply" page, a POST request is sent to "api.ahmedsamy.link".
  - Route 53 redirects this request to API Gateway, which maps the domain to the corresponding API.
  - The API Gateway triggers the "apply" Lambda function, which records the user's information in DynamoDB.

- **Count Page**:
  - Accessing "ahmedsamy.link/count" sends a GET request to "api.ahmedsamy.link".
  - Route 53 redirects this request to API Gateway, which triggers the "count" function.
  - The "count" function retrieves the total number of users from DynamoDB and displays it on the page.

- **Draw Button**:
  - When the "Draw" button is clicked on the "count" page, the API Gateway triggers the "draw" function.
  - The "draw" function randomly selects three users from DynamoDB and updates their `"win"` attribute to `"yes"`, marking them as winners.

## Detailed Steps

For a more detailed breakdown of how the application works, including the exact steps and flow of data, please refer to [this document](https://docs.google.com/spreadsheets/d/1tjw9IJnE3Nu2yNqW-8fJCusx3fskd9W87_LyrrLADKk/edit?usp=sharing).

---

This README provides an overview of your serverless raffle application, detailing its functionality, architecture, and workflow.
