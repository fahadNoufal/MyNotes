```jsx
export const bookData= async ({params})=>{
	
	const { id } = params
	
	const res= await fetch(`....${id}`)
	
	if (!res.ok)
		throw Error('Book does not exist!')
	
	return res.json()
}
```

in router:
```jsx
<Route 
	path=':id' 
	element={<BookItem/>} 
	errorElement={<ErrorEl/>} 
/>
```

ErrorElement.jsx:
```jsx
import {useRouteError} from 'react-router-dom'
export default ErrorEl=()=>{

	const error= useRouteError() 

	return(
		<> ... {error.message} .... </>
	)
}
```

You can also add errorElement to the parent element so that when any child component without errorElement occures an error, then the errorElement handles the error and displays the error Element
						- error bubble up to the parent

ie:
```jsx
<Route path='books' element={<Books/>} errorElement={<ErorrEl/>}>
	<Route path=':id' element={<Book/>} loader={loader}  />
	<Route path='random' loader element={<Rand/>} loader={lo} />
</Route>
```

