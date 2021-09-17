# React Style Guide 

## Table of Contents

  1. [Project Structure Best Practices](#project-structure-best-practices)
  1. [React Component Best Practices](#react-component-best-practices)
  1. [Code Style Best Practices](#code-style-best-practices)
  1. [ReactJS Security Best Practices](#reactjs-security-best-practices)
## **Project Structure Best Practices**
` `React folder structure may differ based on project specification and complexity. There are various react.js best practices that can be taken into account while defining project architecture:

1. **Folder layout**

**ASSETS**:  Store the assets required in your application, any media required in your application.
**COMPONENTS**: Defines the components used in your application, which would be reusable like button, header, footer etc.

**CONSTANTS**: Stores the variable constants that might be used in your application.

**HOOKS**:  Store your custom hooks you create for code reusability, and keeping the code clean

**INTERFACES**: Defines the interfaces for the application used if using typescript to maintain type safety.

**PAGES**: Defines the .jsx files for the application, the pages like login, register, home page etc.

**SERVICES**: Stores services that may be used in your application, for eg: Auth service

**VALIDATIONS**: Stores the validation logic for the application

**NOTE:**

Only include one React component per file.

Always use JSX syntax.

**[⬆ back to top](#table-of-contents)**
### **2. CSS in JS**
In a large project, styling and theming can be a challenging task like maintaining those big scss files. So, the concept of CSS-in-JS solutions ( i.e. put CSS in JavaScript ) came into the picture. Following libraries are based on this concept.

- EmotionJS
- Styled Components
- Glamorous

Among these libraries, you can use based on the requirement like for complicated themes, you can choose styled-components or Glamorous

### **3. Children Props**
Sometimes it is required to render method the content of one component inside another component. So we can pass functions as children props which get called components render function.

### **4. Higher-Order Components (HOC)**
It’s an advanced technique in React which allows reusing component logic inside the render method. An advanced level of the component can be used to transform a component into a higher order of the component. For example, we might need to show some components when the user is logged in. To check this, you need to add the same code with each component. Here comes the use of the Higher-Order Component where the logic to check the user is logged in and keep your code under one app component. While the other components are wrapped inside this.

**5. Custom hooks**

When we want to share logic between two JavaScript functions, we extract it to a third function. Both components and Hooks are functions, so this works for them too!

**A custom Hook is a JavaScript function whose name starts with ”use” and that may call other Hooks.** For example, useFriendStatus below is our first custom Hook:

import { useState, useEffect } from 'react';function useFriendStatus(friendID) { 

` `const [isOnline, setIsOnline] = useState(null); useEffect(() => {

`      `function handleStatusChange(status) {           setIsOnlinestatus.isOnline);      }      ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);      return () => {            ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);      };  });  return isOnline;}

**//using custom hook**

function FriendStatus(props) {    const isOnline = useFriendStatus(props.friend.id);    if (isOnline === null) {        return 'Loading...';    }  

`    `return isOnline ? 'Online' : 'Offline';}

**React component best practices**

Its components are the building blocks of a react project. Here are some of the React best practices that can be considered while coding with React in the component state and component hierarchy.
### **1. Decompose into Small Components**
Try to decompose large components into small components such that component performs one function as much as possible. It becomes easier to manage, test, reuse and create a new small components. This makes sense right?

**For example:**

//bad

class Panel extends React.Component {  	renderHeading() {    		// ...  	  }  	     renderBody() {    	  // ...	  } 	 render() {    		return (      			<div>        			{this.renderHeading()}        			 {this.renderBody()}      		   </div>    		);  	  }}

//good

const PanelHeader = (props) => (    // ...);const PanelBody = (props) => (    // ...);class Panel extends React.Component {    render() {        return (           <div>                // Nice and explicit about which props are used                <PanelHeader title={this.props.title}/>                <PanelBody content={this.props.content}/>           </div>        );    }}

**2. Use Functional Components with Hooks**

After the release of React v16.08, it’s possible to develop **function components with the state** with the new feature **‘React Hooks’**. It reduces the complexity of managing states in Class components. So always prefer to use functional components with React Hooks like useEffect(), useState() etc. This will allow you to repeatedly use facts and logic without much modification in the hierarchical cycle.

### **3. Appropriate Naming and Destructuring Props**
To keep readable and clean code, use meaningful and short names for props of the component. Also, use props destructuring feature of function which discards the need to write props with each property name and can be used as it is.

**For example:**

**const** userProfile =  ({name, title}) => {       **return** ( 	              <div>			<p>{name} – {title}</p>	            </div>	     )}

**Code Style Best Practices**
## **1. Naming convention**
- Extensions: Use .jsx extension for React components.
- Filename: Use PascalCase for filenames. E.g., ReservationCard.jsx.
- Reference Naming: Use PascalCase for React components and camelCase for their instances. eslint: [react/jsx-pascal-case](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

### **2. Avoid the Use of the State as much as Possible**
Whenever using state in the component, keep it centralized to that component and pass it down in the component tree as props.
###
### **3 .Write DRY Code**
Try to avoid duplicate code and create a common component to perform the repetitive task to maintain the DRY (Don’t Repeat Yourself) code structure.

For instance: When you need to show multiple buttons on a screen then you can create a common button component and use it rather than writing markup for each button.

You can also share common logic in your code by using,

- Custom hooks

### **4. Remove Unnecessary Comments from the Code**
Add comments only where it’s required so that you do not get confused while changing code at a later time.

Also don’t forget to remove statements like Console.log, debugger, unused commented code.

**Note: Prefer following proper coding conventions and documentation**
### **5. Use Destructuring to Get Props**
Destructuring was introduced in ES6. This type of feature in the javascript function allows you to easily extract the form data and assign your variables from the object or array. Also, destructuring props make code cleaner and easier to read.

**For example:**

**Example 1:** There is an objecting employee.

|<p>` `const employee= {</p><p>`    `firstName: "Linda",</p><p>`    `lastName: "Cris",</p><p>`    `city: "NY"</p><p>` `}</p>|
| :- |
To access properties of object, you need to write:

|<p>const firstName = employee.firstName</p><p>const lastName = employee.lastName</p><p>const city = employee.city</p>|
| :- |

Which can be written as following with destructuring:

|const { firstName, lastName, city } = employee;|
| :- |

**Example 2:** Let’s take another example. Take an example of a cat that we want to display as a div by naming a class and its type. In between the div, we can see a statement which will tell the cat’s color, its nature-good or bad, etc.

|<p>class Cat extends Component {</p><p>`  `render () {</p><p>`      `const { type, color, badOrGood } = this.props;</p><p>`      `Return <div className={type}>My {color} cat is { badOrGood }</div>;</p><p>`  `} </p><p>}</p>|
| :- |

To maintain clarity with the codes, we can put all the ternary operators in its own variable and see the change.

|<p>class Cat extends Component {</p><p>`  `render () {</p><p>`     `const { type, color, isGoodCat} = this.props;</p><p>`     `const identifier = isGoodCat? "good" : "bad";</p><p>`     `return<div className={type}>My {color} cat is { identifier}</div>;</p><p>`  `} </p><p>}</p>|
| :- |

### **6. Apply ES6 Spread Function**
It would be a more easy and productive way to use ES6 functions to pass an object property. Using {…props} between the open and close tag will automatically insert all the props of the object.

|<p>let propertiesList = {</p><p>`  `className: "my-favorite-props ",</p><p>`  `id: "myFav",</p><p>`  `content: "Hello my favourite!"</p><p>};</p><p>let SmallDiv = props => <div {... props} />;</p><p>let mainDiv = < SmallDiv props={propertiesList} />;</p>|
| :- |
||

You can use the spread function:

- There are no ternary operators required
- There is no need to pass only HTML tag attributes and content

In case of repetitive use of functions, Don’t use the spread function when:

- There are dynamic properties
- There is a need for array or object properties
- In the case of render where nested tags are required

### **7. The Rule of 3**
When there are three or fewer properties, then you should keep those properties in their line inside both the component and the render function.

**Three or fewer:  (Good)**


|<p>let { image, title } = **this**.props;</p><p></p><p><Gallery image="./src/img/image2.jpg" title="Scary Night" /></p><p></p>|
| :- |

**More than three: (bad)**

|<p>let { image, title, artist, class, thumbnail, breakpoint } = **this**.props;</p><p></p><p><Gallery image="./src/img/image2.jpg" title="Scary Night" artist="Vani Garg" class="portrait" thumbnail="./src/img/thumb/night.gif" breakpoint={320} /></p><p></p>|
| :- |

**More than three: (Good)**

The above code becomes unreadable and clumsy. So when there are more than 3 props, write each one in a new line as below :

|<p>let { image,</p><p>`     `title,</p><p>`     `artist,</p><p>`     `class,</p><p>`     `thumbnail,</p><p>`     `Breakpoint</p><p>` `} = **this**.props;</p><p></p>|
| - |
|<p><Gallery </p><p>`         `image="./src/img/image2.jpg"</p><p>`         `title="ScaryNight"</p><p>`         `artist="Vani Garg"</p><p>`         `class="landscape"</p><p>`         `thumbnail="./src/img/thumb/night.gif"</p><p>`         `breakpoint={320} /></p><p></p>|

### **8. Manage too many Props with Parent/Child Component**
It’s a tricky task to manage properties at any level in components, but with the help of React’s state and ES6 destructuring feature, props can be written in a better way as shown below.

**For example:**
Let’s create an application having a list of saved addresses and GPS coordinates of the current location.

The current user’s location should be added in the favourite address and can be kept in parent component App section as shown below:

|class App extends Component {      constructor (props) {         super(props);         this.state = {           currentUserLat: 0,           currentUserLon: 0,           isCloseToFavoriteAddress: **false**         };  }|
| :- |
||

Now, to get data on how close current users are to the favourite address, we will pass at least two props from the App



In render() method of App:

|<FavAddress  ... // Information about the address  addCurrentLat={**this**.state.currentUserLat}  addCurrentLong={**this**.state.currentUserLon} />|
| :- |
||

In the render() for FavAddress Component:

|<p>render () {</p><p>`  `const { addHouseNumber,</p><p>`          `addStreetName,</p><p>`          `addStreetDirection,</p><p>`          `addCity,</p><p>`          `addState,</p><p>`          `addZip,</p><p>`          `addLat,</p><p>`          `addLon,</p><p>`          `addCurrentLat,</p><p>`          `addCurrentLon } = **this**.props;</p><p>`  `**return** ( ... );</p><p>}</p>|
| :- |
||

As you can see in the above infographic, it’s getting unwieldy. It is more feasible to keep multiple sets of options and separate them within their own internal objects.

So, in App constructor:

|<p>**this**.state = { </p><p>`     `currentUserPos: {        lat:0,        lon:0,     },     isCloseToFavoriteAddress: **false**,}</p>|
| :- |
||
At a point before App render():

|<p>const addressList = [];</p><p>addressList.push({</p><p>`     `addHouseNumber: "12344",</p><p>`     `addStreetName: "Street Road",</p><p>`     `addStreetDirection: "N",</p><p>`     `addCity: "My City",</p><p>`     `addState: "ST",</p><p>`     `addZip: "12346",</p><p>`     `addLat: "019782356834",</p><p>`     `addLon: "02384575757"});</p>|
| :- |
||


In App render():

|<FavAddress    addressInfo={addressList[0]}   curretUserPos={**this**.state.currentUserPos}/>|
| :- |

For the FavAddress Component, inside the render function we can see:

||
| :- |

|<p>render () {</p><p>`   `const { addressInfo, currentUserPos } = **this**.props;</p><p>`   `const { addHouseNumber,</p><p>`           `addStreetName,</p><p>`           `addStreetDirection,</p><p>`           `addCity,</p><p>`           `addState,</p><p>`           `addZip,</p><p>`           `addLat,</p><p>`           `addLon } = addressInfo;</p><p>`    `**return** ( ... );</p><p>}</p>|
| :- |

||
| :- |
###
### **9. Use Map Function for Dynamic Rendering of Arrays**
In react, it is possible to create an object with props that return a dynamic HTML block without writing repeated code. For this, react provides a map() function to display arrays in order. While using an array with a map(), one parameter from the array can be used as a key.

|<p>render () {</p><p>`    `const cartoons = [ "Pika", "Squi", "Bulb", "Char" ];</p><p>`    `**return** (      <ul>        { </p><p>`          `cartoons.map(name => <li key={name}>{name}</li>)</p><p>`        `}      </ul>    );</p><p>}</p>|
| :- |
||

Apart from this, ES6 spread functions can be used to send a whole list of parameters in an object by using Object.keys().


|<p>render () {</p><p>`     `const cartoons = {</p><p>`        `"Pika": {            type: "Electric",            level: 10         },        "Squi": {            type: "Water",            level: 10         },        "Bulb": {            type: "Grass",            level: 10         },        "Char": {            type: "Fire",            level: 10        }      };    **return** (       <ul>         {Object.keys(cartoons).map(name => <Cartoons key={name} </p><p>`            `{... cartoon[name]} />)}       </ul>     );}</p>|
| :- |
||
Another example of mapping array is as follow:

|<p>import React, { Component } from "react";</p><p>class Item extends Component { </p><p>` `state = { listitems: [    {         id: 0,        context: "Primary",        modifier: "list-group-item list-group-item-primary"    },    {        id: 1,        context: "Secondary",        modifier: "list-group-item list-group-item-secondary"     },     { </p><p>`        `id: 2,        context: "Success",        modifier: "list-group-item list-group-item-success"     },     {        id: 3,        context: "Danger",        modifier: "list-group-item list-group-item-danger"     },     {       id: 4,       context: "Warning",       modifier: "list-group-item list-group-item-warning"      }   ]     };   render() {   **return**(    <React.Fragment>        <ul className="list-group">           {**this**.state.listitems.map(listitem => (               <li key={listitem.id} className={listitem.modifier}>                   {listitem.context}               </li>            )</p><p>`        `)}       </ul>       </React.Fragment>     );  }}<br>export **default** Item;</p>|
| :- |
||


### **10. Dynamic Rendering with && and the Ternary Operator**
In React, it is possible to perform conditional renderings the same as a variable declaration. For small code with conditions, it’s easy to use ternary operators but with large code blocks, it becomes difficult to find those ternary operators. So the code can be written as below too:


|<p>class FilterResult extends Component {</p><p>`  `render () {</p><p>`    `const { filterResults } = **this**.props;</p><p>`    `**return** (</p><p>`     `<section className="search-results"></p><p>`     `{ filterResults.length > 0 &&</p><p>`       `filterResults.map(index => <Result key={index} {...results[index]/>)     }</p><p>`     `{ filterResults.length === 0 &&</p><p>`         `<div className="no-results">No results</div></p><p>`     `}     </section>   );</p><p>`  `}</p><p>}</p>|
| :- |
||

The above way of conditional rendering will be useful when there are more than 2 conditions or we need to render some code on a specific condition and there is no else part. In those cases, you can use && operators with the condition.
So the above code can be written in true ternary fashion:


||
| :- |

|<p>class FilterResult extends Component {</p><p>`  `render () {</p><p>`    `let { filterResults } = **this**.props;</p><p>`    `**return** (    <section className="search-results"></p><p>`        `{ filterResults.length > 0 &&</p><p>`          `filterResults.map(index => <Result key={index} </p><p>`          `{...results[index] />) </p><p>`       `}      { filterResults.length === 0 && </p><p>`           `<div className="no-results">No results</div> </p><p>`       `}    </section>  );</p><p>`  `}</p><p>}</p>|
| :- |

||
| :- |

Even though the above code is well organized, it could have become messy and unreadable if the render function had more than just one line as there would be more nested brackets.

||
| :- |

|<p>class FilterResult extends Component {</p><p>`   `render () {</p><p>`     `const { filterResults } = **this**.props;</p><p>`     `**return** (        <section className="search-result"></p><p>`       `{ filterResults.length > 0 ? </p><p>`         `filterResults.map(index => <Result key={index} {...                        filterResults[index] />) : </p><p>`         `<div className="no-result">No results</div></p><p>`        `}       </section>    );  }}</p>|
| :- |
||

||
| :- |


As you can see, in both cases code length is the same but there is one main difference, in the first example, there is rapid switching between two different syntaxes making visual parsing difficult as compared to the second, which is simple JavaScript code with variable assignments and one line return function.
It can be inferred from the above code that if the JavaScript is kept inside a JSX object is more than two words (e.g. object. property), then keep that code before the return call.

### **12. Use es-lint or Prettier for Formatting**
Follow the es-lint rules while writing code and use line breaks wherever required for a clean and formatted code. You can also use prettier for formatting the code.

### **13. Write Tests for Each Component**
It is a good practice to write test cases for each component developed as it reduces the chances of getting errors when code is deployed. With the unit testing, you can check all the possible scenarios. Jest or enzymes are the most commonly used react test frameworks.

## **14. Quotes**
Always use double quotes (") for JSX attributes, but single quotes (') for all other JS. eslint: [jsx-quotes](https://eslint.org/docs/rules/jsx-quotes)

**For example:** 

// bad**<**Foo bar**=**'bar' **/>**// good<Foo bar="bar" />
## **15. Spacing**
Always include a single space in your self-closing tag. eslint: [no-multi-spaces](https://eslint.org/docs/rules/no-multi-spaces), [react/jsx-tag-spacing](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-tag-spacing.md)

// bad**<Foo/>**// very bad<**Foo**             />// bad<**Foo** />// good<**Foo** />

## **16. Refs**
- Always use ref callbacks. eslint: [react/no-string-refs](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-string-refs.md)

// bad**<**Foo   ref**=**"myRef"**/>**// good<Foo   ref={(ref) => { this.myRef = ref; }}/>

## **17. Methods**
Use arrow functions to close over local variables

function ItemList(props) { 	 return (    		<ul>     			 {props.items.map((item, index) => (        				<Item          					key={item.key}          				  onClick={() => doSomethingWith(item.name,

index)}       				/>      			))}    		</ul>  	);}

Bind event handlers for the render method in the constructor or use arrow function eslint: [react/jsx-no-bind](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)

**// bad**class extends React.Component { 	 onClickDiv() {    		// do stuff 	 }  	   render() {    		return <div onClick={this.onClickDiv.bind(this)} />; 	}}**// good**class extends React.Component {  	constructor(props) {    		super(props);	 this.onClickDiv = this.onClickDiv.bind(this);  }  	onClickDiv() {    		// do stuff  	  }  		render() {    		   return <div onClick={this.onClickDiv} />; 	   }}

**// good**class extends React.Component {  	  onClickDiv = () => {    		// do stuff  	  }  		render() {    		   return <div onClick={this.onClickDiv} />; 	   }}
## **18. Alignment**
Follow these alignment styles for JSX syntax.

// bad<Foo superLongParam="bar"     anotherSuperLongParam="baz" />// good<Foo    superLongParam="bar"    anotherSuperLongParam="baz"/>// if props fit in one line then keep it on the same line<Foo bar="bar" />// children get indented normally<Foo    superLongParam="bar"    anotherSuperLongParam="baz"   >    <Quux /></Foo>

# **19. React.memo and React.PureComponent**

**React Memo**

When deciding to update DOM, React first renders your component, then compares the result with the previous render. If the render results are different, React updates the DOM.

Current vs previous render results comparison is fast. But you can *speed up* the process under some circumstances.

When a component is wrapped in React.memo(), React renders the component and memoizes the result. Before the next render, if the new props are the same, React reuses the memoized result *skipping the next rendering*.

**For example:** 

export function Movie({ title, releaseDate }) {       return(              <div>                   <div>Movie title: {title}</div>                   <div>Release date: {releaseDate}</div>              </div>      );}export const MemoizedMovie = React.memo(Movie);

**Pure components:**

Pure components is similar to React.memo, where React.memo is used for functional components and pure components are used for class components.

**For example:** 

class App extends React.PureComponent{  	  constructor(props){       		  super(props);       	    this.state = { };     }     render(){          return <div className = "app"> Hello World! </div>     }} 

**ReactJS Security Best Practices**
### **1. Add Security to HTTP Authentication**
There are multiple applications where authentication is done on user login or account creation and this process should be secure as the client-side authentication and authorization can be exposed to many security defects that may destroy these protocols in the application.

The commonly used technique for adding authenticity can be validated using.

1. [JSON Web Token (JWT)](https://jwt.io/)
1. [OAuth](https://oauth.net/2/)
1. [AuthO](https://auth0.com/)
1. [React Router](https://reactrouter.com/)
1. [PassportJs](http://www.passportjs.org/)
### **2. Secure Against Broken Authentication**
Sometimes when you enter authentication details, and the application crashes which might lead to exploitation of user credentials. So to remove this kind of vulnerability, make sure you follow the measures mentioned below.

1. Do use multi-factor and 2-step authorization.
1. You can use cloud-based authentication (for instance Cognito) for secure access.
### **3. Broken Access Control**
With the improper management of restrictions and limitations on authenticated users can cause exploitation of unauthorized data and functionality of a React native app. Sometimes unauthorized users can also change the primary key of data and manipulate the functionality of the application. To ensure security from unauthorized access, follow these practices:

1. Add a role-based authentication mechanism to your react code
1. To secure your application, deny functionality access
### **4. Cross-Site Scripting (XSS)**
1. You can create automated overseeing features that can sanitize the user input
1. Discard malicious and invalid user input from being rendered into the browser.

### **5. Secure Against DDoS Attacks**
The vulnerable security concerns take place when the whole application state management  has loopholes and it masks the IPs. This will restrict the communication caused due to the termination of services. Here are some methods to stop this:

1. Limitation of rate on APIs- This will add limitations to the number of requests for a given IP from a specific source with a complete set of libraries using the Axios-rate limit.
1. Add app-level restrictions to the API.
### **6. SQL Injection**
This attack is related to data manipulation. Due to this vulnerability, attackers can modify any data with or without the user’s permission or can extract any confidential data by [executing arbitrary SQL code](https://www.tatvasoft.com/blog/optimize-sql-query/).
#### **Solution**
1. To eliminate SQL injection attacks, first, validate API call functions against the respective API schemas. In order to handle the issue of time-based SQL injection attacks, you can use timely validation of the schema to avoid any suspicious code injections
1. Another effective way to secure against the SQL vulnerability is by using an SSL Certificate.
### **7. Using dangerouslySetInnerHTML**
In React, you can use ‘innerHTML’ for an element inside DOM which is a risky practice as it’s a wide-open gate for XSS attack. So to remove this issue, React has provided a “dangerouslySetInnerHTML” prop to safeguard against this type of attack.

Also, you can use libraries such as DOMPurify in order to sanitize user input and remove any malicious inputs. React already has an inbuilt function called dependency injection for properly managing user interfaces.
##
##

