---
title: "Fetch API"
date: 2022-10-09T21:53:46+05:30
draft: false
---

- The Fetch API provides a way to fetch resources (including across the network). For making the request and fetching the resources fetch API provides fetch() method. 
- This method is implemented in multiple interfaces. This makes it available in pretty much any context you might want to fetch resources in.
- The fetch() method takes one mandatory argument that is path to the resource want to fetch.


  ```JS 
  fetch("https://pokeapi.co/api/v2/pokemon/1")
  .then((res) => res.json())
  .then((data) => console.log(data));
  ```

- Fetch() method returns a promise that resolves to the response to the request when server responds with headers even if the server response is an HTTP error status.
- Once a response is retrieved, there are multiple methods are available to process response as we want.
- For instance, res.json() method used in above example, it will convert response into json format.