"I'm a developer building a web application and need documentation for the [API Name]. Please provide details on how to:



Authenticate requests using an API key.

Retrieve user data from the /users endpoint.

Include a sample request and response body in JSON format.

Specify the required headers for a successful GET request."



# API Authentication, Endpoints, and Examples
## API Authentication

The NVDB API is generally an open API for reading data.[6, 25] For this reason, a user registration or an API key is not required for most read operations.[25] However, some specific feature types are restricted and do require authentication and authorization.[9]

The documentation for the NVDB API for writing data (NVDB API Skriv) mentions authentication using OpenId Connect, where an idToken (a JSON Web Token or JWT) is used in the Authorization header of requests.[26] The documentation does not specify this method for the public-facing NVDB read API.

It's important to note that the National Vulnerability Database (NVD) is a separate service that does require an API key, which is obtained by providing an organization name and email and agreeing to a terms of use agreement.[27] This is not the same as the NVDB API.

## Retrieving User Data

Based on the available documentation, there is no /users endpoint. The NVDB API is designed to provide access to Norway's national road data, including road objects (/vegobjekter/) and road network information (/vegnett/).[8, 14, 28] The API's purpose is to manage and distribute information about the road network, not user accounts.

## Sample Request and Response

The following is a sample GET request and the type of JSON response you can expect from the NVDB API.

### Sample Request:

GET https://nvdbapiles-v3.atlas.vegvesen.no/vegobjekter/105?inkluder=alle&antall=3
Accept: application/vnd.vegvesen.nvdb-v3-rev1+json
X-Client-Name: MyWebApp
Sample Response Body (JSON):

JSON

{
  "objekter": [
    {
      "long" : "list"
    },
    {
      "of" : "objects"
    }
  ],
  "metadata": {
    "antall": 1001,
    "returnert": 1000,
    "sidestørrelse": 1000,
    "neste": {
      "start": "AEhZez1g4yb",
      "href": "/api-endpoint?start=AEhZez1g4yb"
    }
  }
}
This example shows a partial list of objects with a metadata element that includes details for pagination, such as the total count (antall), the number of items returned on the current page (returnert), and a link to the next page of results (href).[8]

## Required Headers

For a successful GET request, the following headers are recommended or required:

Accept: This header specifies the desired response format, such as application/json or application/xml.[8] The documentation strongly recommends specifying the version explicitly, such as application/vnd.vegvesen.nvdb-v3-rev1+json, to prevent your application from breaking if the format changes.[8, 25]

X-Client-Name: The API maintainers strongly encourage using this header. It provides valuable information about who is using the API, which helps them gather statistics and improve the service.[8, 9]

X-Client-Session: This header is also recommended for tracking individual sessions.[8]

The API's response will also include an X-REQUEST-ID header, which is useful for debugging and for reporting problems to the API maintainers.[8]
