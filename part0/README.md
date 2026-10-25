# Partie 0 — Fondamentaux des applications web

Cours : <https://fullstackopen.com/fr/part0>

Les exercices 0.1 à 0.3 sont des lectures (HTML, CSS, formulaires HTML) et n'ont rien à rendre.

## 0.4 — Nouvelle note (version classique)

Diagramme de ce qui se passe quand l'utilisateur crée une note sur <https://studies.cs.helsinki.fi/exampleapp/notes>.

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    Note right of server: The server adds the new note to the list
    server-->>browser: 302 Found, redirect to /exampleapp/notes
    deactivate server

    Note right of browser: The browser follows the redirect and reloads the page

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: the HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{"content":"note","date":"2026-10-25T15:32:00.449Z"}]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes, including the new one
```

## 0.5 — Application monopage (SPA)

Diagramme de ce qui se passe quand l'utilisateur ouvre <https://studies.cs.helsinki.fi/exampleapp/spa>.

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: the HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "...", "date": "..." }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes

```

## 0.6 — Nouvelle note dans la SPA

Diagramme de ce qui se passe quand l'utilisateur crée une note dans la version SPA.

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note right of browser: The user clicks Save. The JavaScript prevents the default form submission, adds the note to the list and re-renders the notes

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    Note right of browser: Payload: {"content": "...", "date": "..."} as JSON
    activate server
    server-->>browser: 201 Created {"message":"note created"}
    deactivate server

    Note right of browser: No redirect and no page reload: the browser stays on the same page
```
