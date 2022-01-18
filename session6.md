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

![Postman Example](https://github.com/MiriamT/mcon-353/blob/main/images/session6_postman.png?raw=true)

## Call an API in JavaScript using `fetch`

Now that we are familiar with REST APIs and the JSON data format, let's call one using JavaScript's built-in `fetch` function:

```js

```

## Assignment: Create a Chat room
