# LimeSurvey_API_JavaScript_Template

##LimeSurvey RC2 API Example

This example demonstrates how to use LimeSurvey's RemoteControl2 API (LSRC2) in various ways, including through a web page and using Postman. Additionally, it provides instructions for unlocking CORS with the [Access-Control](https://webextension.org/listing/access-control.html) browser extension and configuring CORS on an Apache server.

## Prerequisites

- [LimeSurvey](https://www.limesurvey.org/) installed with RemoteControl2 API enabled.
- Apache server installed (for server-side CORS configuration).
- [Postman](https://www.postman.com/) installed for API testing.

## Usage

1. Open the `index.html` file in a web browser.
2. Modify the `apiUrl`, `username`, and `password` variables in the script to match your LimeSurvey instance.
3. Run the HTML file in a secure environment (e.g., on a web server or using a tool like [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) for VSCode).

## Unlocking CORS with Access-Control Extension

1. Install the [Access-Control](https://webextension.org/listing/access-control.html) browser extension.
2. After installation, click on the extension icon in your browser.
3. Add your LimeSurvey domain to the extension's whitelist to allow cross-origin requests.

## Configuring CORS on Apache Server

If you're running the HTML file on an Apache server and facing CORS issues, you can modify the server configuration to allow cross-origin requests.

### Steps to Modify Apache Configuration

1. Open the Apache configuration file (`httpd.conf`).
2. Locate the `<Directory>` or `<Location>` block that corresponds to your LimeSurvey directory.
3. Add the following lines to enable CORS:

```apache
<Directory "/path/to/limesurvey">
    Header set Access-Control-Allow-Origin "*"
    Header set Access-Control-Allow-Headers "Content-Type"
    Header set Access-Control-Allow-Methods "POST, GET, OPTIONS"
</Directory>
```

Replace `/path/to/limesurvey` with the actual path to your LimeSurvey directory.

4. Save the configuration file and restart the Apache server.

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

### Using Postman

1. Open Postman and create a new request.
2. Set the request method to `POST`.
3. Enter the API endpoint: `https://alegalschi.limesurvey.net/index.php/admin/remotecontrol`.
4. Go to the "Body" tab and select "raw." Paste the following JSON:

```json
{
  "method": "get_session_key",
  "params": ["AleGalSchi", "@Alejos1234@", "Authdb"],
  "id": 1
}
```

5. Click "Send" to make the request.

### Expected Status and Response

For the `get_session_key` request, you should receive a response similar to:

```json
{
  "id": 1,
  "result": "3qiJZo_7tulT5ZG3vCiVjIpzdHLCwg~H",
  "error": null
}
```

## Documentation:

```javascript
// Function to get a session key using the LimeSurvey RemoteControl2 API
async function getSessionKey(username, password) {
    try {
        // Define parameters for the get_session_key method
        const paramsGetSessionKey = {
            method: "get_session_key",
            params: [username, password],
            id: 1,
        };

        // Set up options for the fetch request
        const optionsGetSessionKey = {
            method: "POST",
            body: JSON.stringify(paramsGetSessionKey),
            headers: {
                'Content-Type': 'application/json',
                'Connection': 'Keep-Alive',
                'Host': 'surveys.ak.tu-berlin.de',
                'User-Agent': 'Apache-HttpClient/4.2.2 (java 1.5)',
            },
        };

        // Make a fetch request to the LimeSurvey API endpoint to get the session key
        const response = await fetch(apiUrl, optionsGetSessionKey);

        // Check if the response is successful; otherwise, throw an error
        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }

        // Parse the JSON response
        const data = await response.json();

        // Log the raw response for debugging (commented out by default)
        // console.log('Raw Response:', await response.text());

        // Return the obtained session key
        return data.result;
    } catch (error) {
        // Log and re-throw any errors that occur during the process
        console.error('Error in getSessionKey:', error);
        throw error; // Re-throw the error to propagate it to the caller
    }
}

```
This function, getSessionKey, is responsible for obtaining a session key from the LimeSurvey RemoteControl2 API using the get_session_key method. Here's a breakdown of the key components:

    Parameters:
        username: The LimeSurvey username used for authentication.
        password: The LimeSurvey password associated with the given username.

    API Request Setup:
        The paramsGetSessionKey object is constructed with the necessary parameters for the get_session_key method, including the username, password, and request ID.
        The optionsGetSessionKey object is set up with the method, body (containing the JSON-RPC parameters), and headers required for a LimeSurvey API request.

    Fetch Request:
        A fetch request is made to the LimeSurvey API endpoint (apiUrl) using the configured options.

    Response Handling:
        If the response status is not OK (200), an error is thrown with details about the HTTP error.
        The JSON response is parsed, and the obtained session key is extracted from the response data.

    Error Handling:
        Any errors that occur during the process are logged, and the error is re-thrown to propagate it to the caller.

This function provides a modular and asynchronous way to authenticate with LimeSurvey, ensuring proper error handling and logging for debugging purposes.
