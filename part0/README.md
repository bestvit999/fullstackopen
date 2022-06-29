# web sequence diagram
- https://www.websequencediagrams.com/

# 0.4: New note

```
browser->server: HTTP POST https://studies.cs.helsinki.fi/exampleapp/new_note
note over browser:
request body = 'test content'
end note
server-->browser: status code 302: URL redirect "/exampleapp/notes"

browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/notes
server-->browser: HTML code

browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.css
server-->browser: main.css

browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.js
server-->browser: main.js

note over browser:
exec in 'main.js':
xhttp.open("GET", "/exampleapp/data.json", true)
end note

browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/data.json
server-->browser: [..., {"content":"test content","date":"2022-06-28T22:01:05.688Z"}]

note over browser:
event handler in 'main.js':
xhttp.onreadystatechange = function () {
    1. parse data.json
    2. append each <li> elements to <div id='notes'>
    3. renders page
}
end note
```

# 0.5: Single page app
```
browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/spa
server-->browser: HTML-code
browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.css
server-->browser: main.css
browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/spa.js
server-->browser: spa.js

note over browser:
browser starts executing js-code
that requests JSON data from server 
end note

browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/data.json
server-->browser: [{ content: "HTML is easy", date: "2019-05-23" }, ...]

note over browser:
browser executes the event handler
that renders notes to display
end note
```

# 0.6: SPA new note
```
note over browser:
onsubmit handler :
/* e.preventDefault() to prevent the
 default handling of form submit.
 The default method would send
 the data to the server and cause
 a new GET request, which we don't want to happen. */
 
    1. append 'new note' to 'notes'
    2. redrawNotes()
    3. sendToServer(note)
end note
browser->server: HTTP POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
note over browser:
payload = {
content: "spa_new_note"
date: "2022-06-29T06:01:54.900Z"
}
end note
server-->browser: status code 201
```
