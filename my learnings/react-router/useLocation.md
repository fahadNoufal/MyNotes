```jsx
import {useLocation} from 'react-router-dom'
export default ErrorEl=()=>{

	const location= useLocation() 
	//returns an object with many variables including pathname
	// pathname returns the url path of the page 'contacts/faq/2'
	
	let currentLink=''
	let breadCrumps= location.pathname.split('/')
		.filter(item=>(item!=''))
		.map((crump)=>{
			currentLink+=`/${crump}`
			return (
				<div key={crump}>
					<Link to={currentLink}> {crump} </Link>
				</div>
			)
		})
	return(
		<> ... { breadCrumps } .... </>
	)
}
```