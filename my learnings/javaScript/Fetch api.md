The Fetch API provides an interface for fetching resources (including across the network).

# Using the Fetch API

 It also provides a global `fetch() `method that provides an easy, logical way to fetch resources asynchronously across the network.
 Fetch is promise-based and provides a better alternative that can be easily used in [service worker]

A basic fetch request looks like this:

### Using promise .then

```js
fetch("http://example.com/movies.json")
	.then(res=>res.json())//this returns another promise
	.then(data=>console.log(data))
```

here if you fetch and have an error like 404 , .then statements will still get exicuted. It would not end up in the catch statement, it shows error in console
So we have to do is to inside of respose you have to check to make shure the response is ok 
```js
	.then(res=>{
		if (res.ok){
			console.log("success");
		} else{
			console.log("Not successful")
		}
	})
```

### Using async await

```js
async function logJSONData() {
  const response = await fetch("http://example.com/movies.json");
  const jsonData = await response.json();
  console.log(jsonData);
}
```

The simplest use of `fetch()` takes one argument — the path to the resource you want to fetch — and does not directly return the JSON response body but instead returns a promise that resolves with a `Response` object.
It  in turn, does not directly contain the actual JSON response body but is instead a representation of the entire HTTP response. So, to extract the JSON body content from the [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object, we use the `json()`
method, which returns a second promise that resolves with the result of parsing the response body text as JSON


# fetch() global function

The global **`fetch()`** method starts the process of fetching a resource from the network, returning a promise which is fulfilled once the response is available.

```js
fetch(resource)
fetch(resource, options)
```


# Supplying request options

In order to do more than just fetch data , like to post data , you have to pass in extra options

```js
fetch(url,{
	method:'POST',
	//you need to tell feth that you are going to pass JSON
	headers:{
		'Content-Type':'application/json'
	},
	// We pass in data through the body
	body:JSON.stringify({  // stringify data to send it properly
		name:'User 1'
	})
})
```


The `fetch()` method can optionally accept a second parameter, an `init` object that allows you to control a number of different settings:

```js
// Example POST method implementation:
async function postData(url = "", data = {}) {
  // Default options are marked with *
  const response = await fetch(url, {
    method: "POST", // *GET, POST, PUT, DELETE, etc.
    mode: "cors", // no-cors, *cors, same-origin
    cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
    credentials: "same-origin", // include, *same-origin, omit
    headers: {
      "Content-Type": "application/json",
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: "follow", // manual, *follow, error
    referrerPolicy: "no-referrer", // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    body: JSON.stringify(data), // body data type must match "Content-Type" header
  });
  return response.json(); // parses JSON response into native JavaScript objects
}

postData("https://example.com/answer", { answer: 42 }).then((data) => {
  console.log(data); // JSON data parsed by `data.json()` call
});
```


