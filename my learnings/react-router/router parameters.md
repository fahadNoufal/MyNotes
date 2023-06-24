this is used to pass parameters from url to the react view

``` jsx
<Route path=':id' element={<BookItem/>} > 

in parent view
<Link to={item.id.toString()}> view more </Link>
```

in BookItem.jsx
```jsx
import {useParams} from 'react-router-dom'
export default const BookItem=()=>{
	
	const  {param}= useParams()
	const bookDetails= useLoaderData()
	
	return(
		...... 
		{params}
		{bookDetails}
	)
}

export const bookData= async ({params})=>{
	// react-router-dom will provide arguments which we can destructure. Here we access the 'params' arg which contines all the arguments recieved by the route
	const { id } = params
	// from the params, we destructure 'id' , name of param which we provided
	const res= await fetch(`....${id}`)
	return res.json()
	
}

```