With this we dont have to use local states and event handler functions

```jsx
<Route
	path='help/contact'
	element={<Contact/>}
	action={contactAction}
/> 
```

```jsx
import {Form,redirect} from 'react-router-dom'
export default Contact=()=>{

	const data=useActionData()
	//with this we can access the post request send by the action
	
	return(
		<Form method='post' action='help/contact'>
		//action will toggle function on action property in the specified route Route
			<input type="text" name='email' />
			<input type="text" name='message' />
			{data&& data.error&& <p> {data.error} </p> }
		</Form>
	)
}

//contactAction function to handle form submit
export const contactAction =async ({request})=>{
	//as an argument , we get an object and on that object we get request property . that request contains all of the forms data
	const data= await request.formData()
	const submission={
		email:data.get('email'),
		message:data.get('message')
	}
	console.log(submission)
	
	//send post request
	if (submission.message.length<10){
		return {error:'Message must be over 10 chars long'}
	}
	
	//redirecting the user
	return redirect('/')
}

```

# Navigate

```jsx
if (!userAuthenticated){
	return <Navigate to='/' replace={true} />
}
```
