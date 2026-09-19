### How Does a Browser Communicate with a Backend ?


```txt
Frontend → FastAPI → Database / External API
    ↑                       ↓
    └────── JSON Response ──┘
```

### Learn More 

```txt
┌─────────────────┐
│    FRONTEND     │
│ HTML/CSS/JS     │
│ React, Vue, etc.│
└────────┬────────┘
         │
         │ HTTP Request
         │ (GET, POST, PUT, DELETE)
         ▼
┌─────────────────┐
│     FASTAPI     │
│    BACKEND      │
│                 │
│  API Endpoints  │
│  Business Logic│
└────────┬────────┘
         │
         │
    ┌────┴─────────────┐
    ▼                  ▼
┌───────────┐   ┌──────────────┐
│ DATABASE  │   │ EXTERNAL API │
│ PostgreSQL│   │(Weather API  │
│ MySQL     │   │ Payment API) │
└───────────┘   └──────────────┘
         │                  │
         └────────┬─────────┘
                  │
                  ▼
           Processed Data
                  │
                  ▼
           JSON Response
                  │
                  ▼
┌────────────────────────────┐
│          BROWSER           │
│ Displays the received data │
└────────────────────────────┘

```

## Let 's See What Actually Happens.

### The Browser Loads the Frontend

- Suppose we Opened a website

```txt
https://example.com
```

- The browser sends a request to the server whihc is hosting the website 's  frontend/Client.

Example : 
```txt
GET / HTTP/1.1
Host: example.com
```

- The server returns HTML, CSS, and JavaScript.

Example :
```txt
<h1>Welcome to My Website</h1>
```
- Then The browser renders the page On to Computer Screen.

### Fronted or Client

- Frontend is the user interface.
- It allows the user to interact with the application.


### The Frontend Sends a Request to its Server ( Backend ) 
using API Frameworks eg. ``FastAPI`` , ``Flask``.

- Suppose Website  contains a button.
- When the user clicks the button, website using JavaScript can send a request to Server.

### Frontend logic

```js
async function getUsers() {
    const response = await fetch(
        "http://localhost:8000/users"
    );

    const data = await response.json();

    console.log(data);
}
```

### What Happend via above logic

```txt
User clicks button
       │
       ▼
JavaScript executes
       │
       ▼
fetch() sends HTTP request
       │
       ▼
Server receives request
```



- fetch() is a browser-provided JavaScript API that allows frontend code to make HTTP requests.

- Browser communicates through HTTP.


### Server  Receives the Request

Example : fastapi python server

```py
from fastapi import FastAPI

app = FastAPI()


@app.get("/users")
def get_users():
    return {
        "users": [
            {"id": 1, "name": "Anuj"},
            {"id": 2, "name": "Rahul"}
        ]
    }
```

### What happends when request rach the Server

Example : Python FastAPI Server

- Server Receives the HTTP request.
- It Finds the matching ``/users`` route.
- Executes the ``get_users()`` function.
- Gets the returned results.
- Converts the results into JSON.
- Sends an HTTP response back to the browser.


### Which type of Response Server Sends ?


```py
{
    "users": [
        {"id": 1, "name": "Anuj"},
        {"id": 2, "name": "Rahul"}
    ]
}
```

HTTP response looks like

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "users": [
    {
      "id": 1,
      "name": "Anuj"
    },
    {
      "id": 2,
      "name": "Rahul"
    }
  ]
}
```

### The browser receives the response.

```txt
Server
   │
   │ JSON Response
   ▼
Browser JavaScript
   │
   ▼
response.json()
   │
   ▼
JavaScript Object
   │
   ▼
Update the webpage
```

### Frontend Page Updated.