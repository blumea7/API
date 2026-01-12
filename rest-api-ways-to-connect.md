### Session authentication
  - Use Case: Logging in directly to API UI to manually manage resources in the browser
  - Time Limit
    - Can remain logged in for a prolonged period of time, not just for that HTTP request
    - When a user logs in, a session cookie is created, this means that they can remain logged in when navigating to different pages within automation controller.
  - Sample Procedure (All of this is done by automation controller when you log in to the UI or API in the browser)
    - Get csrftoken by implementing `GET` request in `/api/login/` endpoint
      - Code: `curl -k -c - https://<gateway server name>/api/gateway/v1/login/`
      - Response: `$YOUR_AAP_URL FALSE / TRUE 1780539778 csrftoken GODXonA5LyV1uAs8zvcD2k12DQJC74oB
    - Login to the `/api/login/` endpoint using `username`, `password`, and `X-CSRFToken=<token-value>`
      - Code:  
        `curl -X POST -H 'Content-Type: application/x-www-form-urlencoded' \`  
        `--referer https://<gateway server name>/api/gateway/v1/login/ \`  
        `-H 'X-CSRFToken: <token-value>' \`  
        `--data 'username=admin&password=$YOUR_ADMIN_PASSWORD' \`  
        `--cookie 'csrftoken=GODXonA5LyV1uAs8zvcD2k12DQJC74oB' \`  
        `https://<gateway server name>/api/gateway/v1/login/ -k -D - -o /dev/null`  
    -  Access and test the APIs that need authentication  
       -  `curl -X GET -H 'Cookie: <cookieID>;' https://<gateway server name>/api/controller/v2/settings/all/ -k`
      
### Basic Authentication  
  -  Send **base64-encoded username and password** in each request through the **Authorization Header**  
  -  Sample Basic Authentication with curl:  
      `the --user flag adds this Authorization header for us`
      `curl -X GET --user 'user:password' https://<controller-host>/api/gateway/v1/tokens/ -k -L`


### OAuth2 Authentication
  -  You are given an OAuth 2 token with each API request through the Authorization header
  -  OAuth2 tokens have a configurable timeout and are scopable
  -  Methods to obtain OAuth2 Access Tokens  
     -  Personal Access Tokens
     -  Applicatoin token: Password Grant Type
     -  Application token: Implicit grant type
     -  Application token: Authorizaition Code Grant type
   
  -  Curl Example using Password Grant Type:  
     `curl -u user:password -k -X POST https://<platform-host>/api/gateway/v1/token` //returns a json response with OAuth2 token
     `curl -k -X GET \`  
     `-H “Content-Type: application/json”`  
     `-H “Authorization: Bearer <oauth2-token-value>” \`  
     `https://<platform-host>/api/controller/v2/hosts/`

### Single Sign-on Authentication
  - authentication of the user happens external to automation controller e.g. Google SSO, Microsoft Azure SSO
