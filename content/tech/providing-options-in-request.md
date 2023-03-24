---
title: "Providing Options in Request (Fetch API)"
date: 2022-10-13T21:46:25+05:30
draft: false
---

- fetch() method takes init object as second parameter that allow us to control
a number of different settings.
- We can specify following options in request.
    - method
    - headers
    - body
    - mode 
    - credentials
    - omit
    - same-origin
    - include
    - cache
    - referrer
    - referrerPolicy
    - integrity
    - keepalive
    - signal

- For example, 
    ```JS
        fetch('https://pokeapi.co/api/v2/pokemon/1', {
            method: 'GET',
            headers: { 'Content-Type': 'application/json' },
            mode: 'no-cors',
            cache: 'no-cache',
            credentials: 'same-origin' })
        .then(data => data.json())
        .then(pokemons => console.log(pokemons));
    ```
    