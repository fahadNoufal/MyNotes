
# Promise

The promise is a special type of JS object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value

For eg:
	if you request an information from an remote api , then you will immidiately given a promise that that task will eventually be complete or filed . Its untill some time later the promise itself is actually resolved or rejected and you can use the result of that promise

```
//handle fulfilled (resolved) promises
promise.then((result)=>{....})

//handle failed (rejected) promises
promise.catch((error)=>{....})
```

#### These .then and .catch will wait untill the promise returns a result or an error

eg:
```js
const axiosRequest = require('axios')

axiosRequest
	.get('url of a site to fetch data')
	.then(response=>{
		console.log(`succussfuly recieved response ${response}`)
	})
	.catch(error=>{
		console.log(`error occured : ${error}`)
	})

console.log('process completed')
```

Here , we recieve `process completed` even before we recieve `successful`  or `error occured` . this is because they waits to complete the promise while the next line gets exicuted


# async and await

The awit operator is used to wait for a `Promise` to complete before moving to the next line . 
`this makes our code lot neat and easier to read`
It can only be used inside an `async function`  within regular JS code;
However it can be used on its own with JS modules

```js
const axiosRequest = require('axios')

async function(){
	try{
		let response= await axiosRequest.get('url of a site to fetch data')
		console.log(response)
	} catch(error){
		console.error(`ERROR : ${error}`)
	}
}
console.log('process completed')
```

#### Here everything happens in the correct order
