 b#summary
	highly dynamic
		state and components changing
		state- change information on the spot
			renders specific components 

	state is changable
		prop is not
		(you can hardcode or inherit props)

	sharing info
		push to an ancestor

	Working with js. Kinda like super Ajax
	Uses JSX expressions
		they become reglar JS objects as a result
		eg
		
		const user = {
			firstName: simon
			lastName:  brady
		};


		`function formatName(user){
			return user.firstName = ' ' user.lastName
		};`


		`function getGreeting(user){
			if(user){
				return <h1>hello, {firstName(user)}</h1>
			}
			return <h1> hello, stranger </h1>
		};`

		const element = {
			<h1>{getGreeting(user)}</h1>
		}

		React.DOM.render(
			element,
			document.getElementById('root')
			);
# Varaible attributes in JSX
	const goose = "url"

	const gooseImg = (
		<img src = { goose } />
		);

	ReactDOM.render(
		gooseImg,
		document.getElementById('app')
		);

React Facebook Boilerplate
	check this out for a quickstart guide.

Tic Tac Toe

react rails gem

Rendering Elements
	building blocks of React applications
	const element = <h1>hello</h1>
		--> element
		--> plain objects, easy to create
			--> elements vs components?
				elements are what components are made of

	consider the <div id='root'></div>
		--> homebase of the application, everything thta happens inside managed by the React DOM

	ReactDOM.render(
		element,
		document.getElementById('root')
		);

		--> would render 'hello' to the root DOM


		function tick() {
		  const element = (
		    <div>
		      <h1>Hello, world!</h1>
		      <h2>It is {new Date().toLocaleTimeString()}.</h2>
		    </div>
		  );
		  ReactDOM.render(
		    element,
		    document.getElementById('root')
		  );
		}

		setInterval(tick, 1000); --> set interval is a callback function
--------------------------------------------------------------------------
components and props

	function Welcome(props) {
	  return <h1>Hello, {props.name}</h1>;
	}

	funciton is valid React. Accepts a single 'props' object argument with data and returns a React element. -- Functional


	class Welcome extends React.Component {
		render() {
		    return <h1>Hello, {this.props.name}</h1>;
		}
	}

	same as the last one, using more ES6 JS to define a class.


	function Welcome(props) {
	 return <h1>Hello, {props.name}</h1>;
	}

	const element = <Welcome name="Sara" />;
	ReactDOM.render(
	  element,
	  document.getElementById('root')
	);


	"Let's recap what happens in this example:

	We call ReactDOM.render() with the <Welcome name="Sara" /> element.
	React calls the Welcome component with {name: 'Sara'} as the props.
	Our Welcome component returns a <h1>Hello, Sara</h1> element as the result.
	React DOM efficiently updates the DOM to match <h1>Hello, Sara</h1>"
----------------------------------------------------------------------------------
'lil twitter
	--> look into redux
	fully functioning rails application
	front end is styled
	index.erb
		--> all static information

twitter
	globals, username and avatar
		used in everything!
		could be put into the app class, OR into the redux store


figuring out the endpoints
	checkout your routes
		tweets/recent
		hashtags.popular

Everything needs componentized
	will be using hard coded data

using react rails
	install gem react-rails
		add it to the gemfile
		$ bundle
		$ bin/rails g react:install

			uses the asset pipeline
			JSX transformer
				JSX--> what is it
					used to write the HTML that gets rendered
			gives you a component file
			alters your app file 
				gives you a manifest, adds 'react shit'
					looks like its commented out, but it works with the asset pipeline
				each, except images, has a manifest
			server rendering --> look it up later

step 1.
	want a tweet
		put a tweet file into your component folder
		components/Tweet.es6.jsx (good for documentation, a little bloated)

		class Tweet extends React.Component --> dont need to require React since the gem takes care of it


	class Tweet extends React.Component {
		render(){
			return(
				hello world< /h1>
			)
		}
	}

	-->became a react object

	how to render in rails

		export default Tweet (within the file (Tweet.jsx)) -->. dont necissary need import or export when using this gem
		
		<%= react_component('Tweet')%>

		class Tweet extends React.Component {
		render(){
			let data = {avatar: nasdfj}
			return(
				<div>
				hello world< /h1>
				className= "avatar" src={data.avatar}</ div>
				</ >
			)
		}
	}

	passing into this so its reusable, using props
		back to the erb syntax <%= react_component('Tweet' data...) --> as opposed to having it in the jsx file

in the console, use $r at the end of the props

destructure
	class Tweet extends React.Component {
	render(){
		const {avatar, fullName, username, content, timestamp} = this.props
			let data = {avatar: nasdfj}
			return(
				<div>
				hello world< /h1>
				className= "avatar" src={avatar}</ div>
				</ >
			)
		}
	}

	not good practice to reference your props within JSX

timeline

	class Timeline extends React.Component{
		render(){
			return(
				<ul>
					<Tweet />
				</ul>
			)
		} 
	}

consider doing multiple tweets with an array of data
	{ tweets.map((tweet) => )
		<Tweet 
			/>
		}


componentize the entire lil twitter
	everything under 'App'
---------------------------------------------------------------------------------------------------

Ajax and react
	1. page loads
	2. component app loads
	3. upon loading, hit the api, get data
		before all this 'componentDidMount(){
		}'
	4. save data as a state (changes as opposed to props)

saving state
need a constructor function --> Similar to ruby initialize
	want to alter our state, and define the different states

	so! under class App extends React.Component{
		constructor(){
			super() --> pulling from react component
			this.state= {
				tweets:[]
				trends: ['stuff...']
				tweetContent:''
			}
		}
		this.handleOnChange = this.handleOnChange.bind(this)
		this.handleOnSubmit = this.handleOnSubmit.bind(this)

		handleOnChange(event){
			this.setState({tweetContent: event.target.value})
		}
		handleSubmit(e){
			e.preventDefault()
			const { tweetContent } = this.state
			$.ajax({
				url:'/tweets',
				method: 'posts,
				data: {tweet: {content: tweetContent}}'
				}).done((res) => {
					this.setState({tweets:[res].concat(this.state.tweets)})
					})
		}
		componentDidMount(){
			$.ajax({
				url: (where to go to for data),
				method: 'get'
			}).done((res) =>{
				this.setStatetrends: res})
			})
			$.ajax({
				url:'/hastags/popular',
				})
		}
	}


Ajax call--> should learn fetch
	componentDidMount(){
	$.ajax({
		url: (where to go to for data)
		method: 'get'
		}).done((res) =>{
			this.setStatetrends: res})
		})

	})
	}

-------------------------------------------------------------------------------------------------

Ajax React and Search functions

-------------------------------------------------------------------------------------------------

Instagram
	likes
	pics
	users


	person has many pictures
	pictures belong to a user
	pictures have many likes

-----------------------------------------------------------------------









