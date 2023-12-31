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

## Apache CORS Configuration

If you encounter CORS issues, you may need to configure your Apache HTTP server to allow cross-origin resource sharing. Add the following lines to your Apache configuration:

```apache
<IfModule mod_headers.c>
    Header set Access-Control-Allow-Origin "*"
    Header set Access-Control-Allow-Methods "GET, POST, PUT, DELETE, OPTIONS"
    Header set Access-Control-Allow-Headers "Origin, X-Requested-With, Content-Type, Accept, Authorization"
    Header always set Access-Control-Allow-Headers "Content-Type"
</IfModule>
```
## Using Apache with CORS Unlock Tool

To unlock CORS for your LimeSurvey instance, you can also use the Access-Control-Allow-Origin tool. Follow the tool's documentation to set up and configure it for your environment.
## Steps

### 1. Get Session Key

The `get_session_key` function is used to obtain a session key. Replace `username` and `password` with your LimeSurvey admin credentials.

```javascript
const sessionKey = await getSessionKey(username, password);
```
https://manual.limesurvey.org/RemoteControl_2_API

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
  "params": ["username", "password", "Authdb"],
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

**Updated Sample Request Result and Explanation:**

```json
{
    "sid": "853721",
    "owner_id": "1",
    "gsid": "1",
    "admin": "inherit",
    "active": "Y",
    "expires": null,
    "startdate": null,
    "adminemail": "inherit",
    "anonymized": "N",
    "format": "S",
    "savetimings": "Y",
    "template": "inherit",
    "language": "en",
    "additional_languages": "de",
    "datestamp": "Y",
    "usecookie": "I",
    "allowregister": "I",
    "allowsave": "I",
    "autonumber_start": "1",
    "autoredirect": "Y",
    "allowprev": "I",
    "printanswers": "I",
    "ipaddr": "Y",
    "ipanonymize": "N",
    "refurl": "Y",
    "datecreated": "2023-11-13 12:56:54",
    "showsurveypolicynotice": "0",
    "publicstatistics": "I",
    "showdatapolicybutton": "0",
    "showlegalnoticebutton": "0",
    "publicgraphs": "I",
    "listpublic": "I",
    "htmlemail": "I",
    "sendconfirmation": "I",
    "tokenanswerspersistence": "I",
    "assessments": "I",
    "usecaptcha": "E",
    "usetokens": "N",
    "bounce_email": "inherit",
    "attributedescriptions": null,
    "emailresponseto": "inherit",
    "emailnotificationto": "inherit",
    "tokenlength": "-1",
    "showxquestions": "N",
    "showgroupinfo": "I",
    "shownoanswer": "I",
    "showqnumcode": "I",
    "bouncetime": null,
    "bounceprocessing": "N",
    "bounceaccounttype": null,
    "bounceaccounthost": null,
    "bounceaccountpass": null,
    "bounceaccountencryption": null,
    "bounceaccountuser": null,
    "showwelcome": "Y",
    "showprogress": "Y",
    "questionindex": "-1",
    "navigationdelay": "-1",
    "nokeyboard": "I",
    "alloweditaftercompletion": "I",
    "googleanalyticsstyle": null,
    "googleanalyticsapikey": null,
    "tokenencryptionoptions": "{ \"enabled\":\"Y\",\"columns\":{ \"firstname\":\"N\",\"lastname\":\"N\",\"email\":\"N\" } }"
}
```



- The `Sample Request Result` represents the properties of the LimeSurvey with Survey ID 853721 retrieved through a sample API request.
- Below are key properties and their values:
  - `sid`: Survey ID is "853721".
  - `owner_id`: Owner ID is "1".
  - `gsid`: GSID is "1".
  - `admin`: Admin settings are "inherit".
  - `active`: Survey is "active" (Y).
  - `expires`: Survey expiration is not set (null).
  - `startdate`: Survey start date is not set (null).
  - `adminemail`: Admin email settings are "inherit".
  - ... (and many more survey properties).

- Date-related properties:
  - `datecreated`: Survey creation date is "2023-11-13 12:56:54".
  - `expires`: Expiration date is not set (null).
  - `startdate`: Start date is not set (null).
  - `bouncetime`: Bounce time is not set (null).

- Other notable settings:
  - `language`: Survey language is "en".
  - `additional_languages`: Additional languages include "de".
  - `tokenencryptionoptions`: Token encryption is enabled with specific column settings.

- The response provides a comprehensive overview of the survey's configuration and settings. Refer to LimeSurvey documentation for details on each property.
