# LimeSurvey_API_JavaScript_Template

## LimeSurvey RC2 API Example

This example demonstrates how to authenticate with the LimeSurvey RemoteControl2 API (LSRC2) and make a sample API request using JavaScript in a web environment. This can serve as a starting point for integrating LimeSurvey's API into your applications.

## Prerequisites

- [LimeSurvey](https://www.limesurvey.org/) installed with RemoteControl2 API enabled.

## Usage

1. Open the `index.html` file in a web browser.
2. Modify the `apiUrl`, `username`, and `password` variables in the script to match your LimeSurvey instance.
3. Run the HTML file in a secure environment (e.g., on a web server or using a tool like [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) for VSCode).

## Steps

### 1. Get Session Key

The `get_session_key` function is used to obtain a session key. Replace `username` and `password` with your LimeSurvey admin credentials.

```javascript
const sessionKey = await getSessionKey(username, password);
```

### 2. Make a Sample API Request

Adjust the `makeSampleRequest` function to perform the desired API request. In this example, it fetches survey properties for a specified survey ID.

```javascript
const surveyId = 853721;  // Replace with your survey ID
const sampleRequest = await makeSampleRequest(sessionKey, surveyId);
```

## Note

- Ensure that LimeSurvey's CORS (Cross-Origin Resource Sharing) settings allow requests from the origin where the HTML file is hosted.
- Customize the script according to your specific use case and API endpoints.

