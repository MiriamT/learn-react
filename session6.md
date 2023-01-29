# Session 6: Fetching Data from APIs

## Objectives

- What is an API?
- Call an API with the Postman app
- Call an API in JavaScript using `fetch`
- Assignment: Create a Chat room

## What is an API?

An Application Programming Interface enables software programs to talk to each other using a defined set of communications rules. [Web APIs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Introduction) are standards for how a web app interacts with its backend to send and receive data based on user interaction. [REST APIs](https://restfulapi.net/) are commonly used for this purpose.

The simplest way to call a REST API is to open a url in your browser. For example, click [here](http://api.plos.org/search?q=title:DNA) to open up a REST GET request that will return a [JSON](https://www.json.org/json-en.html) response in your browser window. It should look something like this:

```json
{
  "response": {
    "numFound": 5528,
    "start": 0,
    "maxScore": 6.567992,
    "docs": [
      {
        "id": "10.1371/journal.pone.0000290",
        "journal": "PLoS ONE",
        "eissn": "1932-6203",
        "publication_date": "2007-03-14T00:00:00Z",
        "article_type": "Research Article",
        "author_display": [
          "Rayna I. Kraeva",
          "Dragomir B. Krastev",
          "Assen Roguev",
          "Anna Ivanova",
          "Marina N. Nedelcheva-Veleva",
          "Stoyno S. Stoynov"
        ],
        "abstract": [
          "Nucleic acids, due to their structural and chemical properties, can form double-stranded secondary structures that assist the transfer of genetic information and can modulate gene expression. However, the nucleotide sequence alone is insufficient in explaining phenomena like intron-exon recognition during RNA processing. This raises the question whether nucleic acids are endowed with other attributes that can contribute to their biological functions. In this work, we present a calculation of thermodynamic stability of DNA/DNA and mRNA/DNA duplexes across the genomes of four species in the genus Saccharomyces by nearest-neighbor method. The results show that coding regions are more thermodynamically stable than introns, 3′-untranslated regions and intergenic sequences. Furthermore, open reading frames have more stable sense mRNA/DNA duplexes than the potential antisense duplexes, a property that can aid gene discovery. The lower stability of the DNA/DNA and mRNA/DNA duplexes of 3′-untranslated regions and the higher stability of genes correlates with increased mRNA level. These results suggest that the thermodynamic stability of DNA/DNA and mRNA/DNA duplexes affects mRNA transcription."
        ],
        "title_display": "Stability of mRNA/DNA and DNA/DNA Duplexes Affects mRNA Transcription",
        "score": 6.567992
      }
    ]
  }
}
```

> **Note:** Install the [JSONVue](https://chrome.google.com/webstore/detail/jsonvue/chklaanhfefbnpoihckbnefhakgolnmc?hl=en-US) Chrome extension for automatic json formatting.

You can also use the `curl` command in your terminal to call REST APIs. This command will fetch the current weather for New York by its zip code:

```
curl "https://api.openweathermap.org/data/2.5/weather?zip=10282,us&appid=XXXXX"
```

Output:

```
StatusCode        : 200
StatusDescription : OK
Content           : {"coord":{"lon":-73.7126,"lat":40.6321},"weather":[{"id":804,"main":"Clouds","description":"overcas
                    t clouds","icon":"04n"}],"base":"stations","main":{"temp":275.18,"feels_like":272.36,"temp_min":273
                    .6...
RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    X-Cache-Key: /data/2.5/weather?q=woodmere
                    Access-Control-Allow-Origin: *
                    Access-Control-Allow-Credentials: true
                    Access-Control-Allow-Methods: GET, POST
                    Con...
Forms             : {}
Headers           : {[Connection, keep-alive], [X-Cache-Key, /data/2.5/weather?q=woodmere],
                    [Access-Control-Allow-Origin, *], [Access-Control-Allow-Credentials, true]...}
```

To try it yourself, sign up for a weather API key [here](https://openweathermap.org/api) and replace `appid=XXXXX` with your API key.

## Call an API with the Postman app

[Postman](https://www.postman.com/downloads/) is a great tool for exploring REST APIs. Install Postman and use it to call one the apis above:

![Postman Example](https://github.com/MiriamT/learn-react/blob/main/images/session6_postman.png?raw=true)

## Call an API in JavaScript using `fetch`

Now that we are familiar with REST APIs and the JSON data format, let's call one using JavaScript's built-in `fetch` function:

```js
fetch(
  "https://api.openweathermap.org/data/2.5/weather?zip=10282,us&appid=XXXXX"
)
  .then((response) => response.json()) // pull the json out of the response
  .then((data) => console.log(data)); // get the json data as a javascript object
```

`fetch` is based off of [JavaScript Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), which are asynchronous. When the promise resolves at some future time, it will run the code in the `.then()` function. Sometimes a promise will return another promise, so you can "chain" the `.then()` calls to resolve subsequent promises. In the code snippet above, `response.json()` returns another promise so `.then()` is called a second time to process the data that the second promise returns.

> **Assignment:** Read more about [JavaScript's Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

`fetch` will call the HTTP `GET` method type by default. To call a different [HTTP method](https://restfulapi.net/http-methods/) and send data as part of the API call, you would write something like this:

```js
const data = {...};

fetch(url, {
  method: "POST", // *GET, POST, PUT, DELETE, etc.
  headers: {
    "Content-Type": "application/json", // tells REST that we will send the body data in JSON format
  },
  body: JSON.stringify(data),
}).then(...);
```

## Assignment: Create a Chat room

Create a new top-level component named `<Chat>` nested under the main `<App>`. The `<Chat>` component should be rendered at the `/chat` path, and a "Chat" link should be added to the app header to render this new page.

The `<Chat>` page will use APIs to send and receive chatroom messages. It should enable users to:

1. Create a username
2. Create a new chatroom
3. See messages displayed in a chatroom
4. Post messages to a chatroom

The author has built APIs on AWS to manage the backend data, your UI just needs to call them:

- GET /chats
- GET /chats/{id}/messages
- PUT /chats
- PUT /messages

### GET /chats

Returns all the chat rooms as an array of objects.

### GET /chats/{id}/messages

Returns all the messages in the chatroom with the given `id` as an array of objects.

For example: `/chats/class/messages` would return messages for a chatroom that has an `id` with a value of `class`.

### PUT /chats

Creates a new chat with the data provided in the body, and returns the created chat object.

Example body:

```js
{
  id: 'newChat', // required
  name: 'New Chat' // required
}
```

Example response:

```js
{
  // same data is returned
  id: 'newChat',
  name: 'New Chat'
}
```

### PUT /messages

Creates a new message with the data provided in the body, and returns the created message object.

Example body:

```js
{
  chatId: 'newChat', // required, must be an existing chat id
  username: 'newUser', // required
  text: 'hello!' // required
}
```

Example response:

```js
{
  // new data is returned
  chatId: 'newChat',
  username: 'newUser',
  text: 'hello!',
  id: 'ae34a5c7-4704-4246-b5b9-2d3d06c4e189', // id created by the server
  isoDate: '2022-01-19T01:36:40.068Z', // timestamp (in ISO Date format) created by the server
}
```

### Calling the APIs

The base url for the API calls is: `https://z36h06gqg7.execute-api.us-east-1.amazonaws.com/`

Below is an example `fetch` call to get the chats:

```js
fetch("https://z36h06gqg7.execute-api.us-east-1.amazonaws.com/chats")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

This PUT call will create a new chat:

```js
const chat = {
  id: 'secret',
  name: 'Secret Club'
};

fetch('https://z36h06gqg7.execute-api.us-east-1.amazonaws.com/chats', {
  method: "PUT",
  headers: {
    "Content-Type": "application/json", // tells REST that we will send the body data in JSON format
  },
  body: JSON.stringify(chat),
}).then(...);
```
