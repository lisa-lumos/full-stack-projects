# React.js
React is a `JavaScript library` for building `user interfaces`. It is a `front end` framework. It makes it easy to create repetitive elements. You can break down a very complex user interface structure into a `component tree`, with each of the component `reusable` and `customizable`. It also vastly simplifies the structure of your website. 

It is effectively like creating your own custom HTML elements. React combines a small amount of html, css and javascript together in to a single component so that each component has its own styling, functionality. We can also have component `listening` for changes in the server and updating itself and its own appearance and data, and talk to the server independently. 

React is also able to render changes effectively  because it compares changes, and makes your app more interactive and much faster.  

## JSX and Babel
In the html file, `<div id="root"></div>` is the root of your React app, everything we create using React is going to be inserted in this div. 

The html file in "public" folder contains below contents, and will not be modified. All code will be written in JavaScript using React. 
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>JSX</title>
    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <div id="root"></div>
    <script src="../src/index.js" type="text/javascript"></script>
  </body>
</html>
```
For index.js file inside the "src" folder, install `react` and `react-dom` dependencies. 
```
import React from "react";
import ReactDOM from "react-dom";

ReactDOM.render(
  <div>
    <h1>Hello World!</h1>
    <p>This is a paragraph.</p>
  </div>,
  document.getElementById("root")
);

```
Babel is a Javascript compiler. It can take next gen JavaScript like es6, 7, 8, with arrow functions, map functions, etc, to a version of JavaScript that every browser can understand. 

Note that when we use the `render` method, it can only take a single html element. So if we need to render a few elements, we can enclose all of them into a single `div` element. 

## Javascript Expressions in JSX
JSX lets us add html inside a javascript, and then insert javascript inside that html. 
```
import React from "react";
import ReactDOM from "react-dom";

const fName = "Lisa";
const lName = "Lumos";

ReactDOM.render(
  <div>
    <h1>Hello {fName + " " + lName}!</h1>
    <p>Your lucky number is {Math.floor(Math.random()*10)}</p>
  </div>,
  document.getElementById("root")
);
```
You can put expressions inside curly braces, but statements like if-else wouldn't work. The part `{fName + " " + lName}` can be replaced by `{fName} {lName}`, or ``{`${fName} ${lName}`}``. 

## JSX Attributes, and Styling React Elements
We are writing html inside javascript, to the file is no longer a plain old javascript file, it is a jsx file. To let the browser know it,in html file, we need to change `<script src="../src/index.js" type="text/javascript"></script>` to `<script src="../src/index.js" type="text/JSX"></script>`. 

To include css in jsx file: 
```
import React from "react";
import ReactDOM from "react-dom";

const img = "https://picsum.photos/200";

ReactDOM.render(
  <div>
    <h1 className="heading">My Favourite Foods</h1>
    <img alt="random" src={img + "?grayscale"} />

    <img
      className="food-img"
      alt="bacon"
      src="https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/delish-190621-air-fryer-bacon-0035-landscape-pf-1567632709.jpg?crop=0.645xw:0.967xh;0.170xw,0.0204xh&resize=480:*"
    />
  </div>,
  document.getElementById("root")
);
```
Note that instead of `class`, we use attributes like `className`, which is camel cased. 

And in css file:
```
.heading {
  color: red;
}

.food-img {
  height: 100px;
  width: 100px;
}
```

## Inline Styling for React Elements
You might want to change the styles of html element on the fly while you app is running, this is when inline styling becomes useful. 
```
import React from "react";
import ReactDOM from "react-dom";

const customStyle = {
  color: "red",
  fontSize: "20px",
  border: "1px solid black"
};

customStyle.color = "blue";

ReactDOM.render(
  <h1 style={customStyle}>Hello World!</h1>,
  document.getElementById("root")
);

```

## React Components
Components allow us to split up a large file or a complex web structure into smaller components, and we can reuse each of these components when we need the same functionality. 

React convention for function is to name is in Pacal case so that each word has the first letter capitalized. This allow the React to discern the custom components and the original html elements:
```
import React from "react";
import ReactDOM from "react-dom";

function Heading() {
  return <h1>My Favourite Foods</h1>;
}

ReactDOM.render(
  <div>
    <Heading />
    <ul>
      <li>Bacon</li>
      <li>Jamon</li>
      <li>Noodles</li>
    </ul>
  </div>,
  document.getElementById("root")
);
```
Note that the `Heading` component has no contents, so write it as a self-closing tag. Follow Airbnb Style Guide for React `https://github.com/airbnb/javascript/tree/master/react` for best practices. 

We can use a ES6 feature to import Heading component from a separate file. Inside the "src" folder, create a new file "Heading.jsx". The convention specifies that we usually leave index.js as a plain js file, even we use some React and some jsx in it; but we have all components separated into individual files with a jsx extension. 
```
import React from "react"

function Heading() {
  return (<h1>My Favourite Foods</h1>);
}

export default Heading;
```
And in index.js:
```
import React from "react";
import ReactDOM from "react-dom";
import Heading from "./Heading"

ReactDOM.render(
  <div>
    <Heading />
    <ul>
      <li>Bacon</li>
      <li>Jamon</li>
      <li>Noodles</li>
    </ul>
  </div>,
  document.getElementById("root")
);
```
Often, this is what you see in the index.js file:
```
import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App";

ReactDOM.render(<App />, document.getElementById("root"));
```
And a custom file called App.jsx in src/components folder, with other jsx files:
```
import React from "react";
import Heading from "./Heading";
import List from "./List";

function App() {
  return ( // Note the quote!
    <div>
      <Heading />
      <List />
      <List />
    </div>
  );
}

export default App;
```

## Javascript ES6 Import, Export and Modules
In index.js file:
```
import React from "react";
import ReactDOM from "react-dom";
import pi, {doublePi, triplePi} from "./math.js";

ReactDOM.render(
  <ul>
    <li>{pi}</li>
    <li>{doublePi()}</li>
    <li>{triplePi()}</li>
  </ul>,
  document.getElementById("root")
);
```
In math.js file, note that you can call the default export anything, but you cannot do this to the non-default imports:
```
const pi = 3.1415962;

function doublePi() {
  return pi * 2;
}

function triplePi() {
  return pi * 3;
}

export default pi; // This is the default exports
export { doublePi, triplePi }; // this is the non-default exports
```
Note that when working with Node, we are not sure that we can always use ES6, because the browser penetration of ES6 is something like 80% at the moment. 

## Local Environment Setup for React Development (for mac)
1. Install the latest version of Node. `node --version`. 
2. Install VSCode. Install Babel Javascript extension for highlighting, and Vscode-icons extension for file structure icons. 
3. Create a React app. `https://reactjs.org/docs/create-a-new-react-app.html`. 
```
npx create-react-app my-app
cd my-app
npm start
```
4. Run the app. Follow instructions in step 3. 

Go to VSCode and add this folder. Now delete all files in the public folder, except index.html. And in the src folder, we only keep index.js file. In the head section of index.html, only keep `<meta charset="utf-8" />` and `<title>React App</title>`, and in the body section, only keep `<div id="root"></div>`. Now link index.js into the body: `<script src="./src/index.js" type="text/jsx"></script>`. So now index.html file looks like this:
```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8" />
  <title>React App</title>
</head>

<body>
  <div id="root"></div>
  <script src="./src/index.js" type="text/jsx"></script>
</body>

</html>
```
And in index.js, have this:
```
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <h1>Hello World!</h1>,
  document.getElementById("root")
);

```
When you download projects from websites, could use `npm-check-updates` to update the outdated packages. 

## React Props (Properties)
We can remove the hard coded part of react components, and instead pass values as `props` into them. This enables us to reuse the components. Customize React elements could have customized properties. It is almost like calling a function. For example, in index.js file:  
```
import React from "react";
import ReactDOM from "react-dom";

function Card(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <img src={props.img} alt="avatar_img" />
      <p>{props.tel}</p>
      <p>{props.email}</p>
    </div>
  );
}

ReactDOM.render(
  <div>
    <h1>My Contacts</h1>
    <Card
      name="Beyonce"
      img="https://blackhistorywall.files.wordpress.com/2010/02/picture-device-independent-bitmap-119.jpg"
      tel="+123 456 789"
      email="b@beyonce.com"
    />
    <Card
      name="Jack Bauer"
      img="https://pbs.twimg.com/profile_images/625247595825246208/X3XLea04_400x400.jpg"
      tel="+7387384587"
      email="jack@nowhere.com"
    />
  </div>,
  document.getElementById("root")
);
```
Note that you cannot add `className` as html attribute into customized elements, you can only add it to original html components. Because it will think this `className` is a customized property name. Note that if we need to pass javascript objects in props inside ReactDOM.render(), need to use curly braces such as {object.attribute}. 

## More Moduler code, and React DevTools
In index.js:
```
import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App";

ReactDOM.render(<App />, document.getElementById("root"));
```
In App.jsx:
```
import React from "react";
import Card from "./Card";
import contacts from "../contacts";
import Avatar from "./Avatar";

function App() {
  return (
    <div>
      <h1 className="heading">My Contacts</h1>
      <Avatar img="https://pbs.twimg.com/profile_images/744849215675838464/IH0FNIXk.jpg" />
      <Card
        name={contacts[0].name}
        img={contacts[0].imgURL}
        tel={contacts[0].phone}
        email={contacts[0].email}
      />
      <Card
        name={contacts[1].name}
        img={contacts[1].imgURL}
        tel={contacts[1].phone}
        email={contacts[1].email}
      />
      <Card
        name={contacts[2].name}
        img={contacts[2].imgURL}
        tel={contacts[2].phone}
        email={contacts[2].email}
      />
    </div>
  );
}

export default App;
```
In Avator.jsx:
```
import React from "react";

function Avatar(props) {
  return <img className="circle-img" src={props.img} alt="avatar_img" />;
}

export default Avatar;
```
In Card.jsx:
```
import React from "react";
import Avatar from "./Avatar";
import Detail from "./Detail";

function Card(props) {
  return (
    <div className="card">
      <div className="top">
        <h2 className="name">{props.name}</h2>
        <Avatar img={props.img} />
      </div>
      <div className="bottom">
        <Detail detailInfo={props.tel} />
        <Detail detailInfo={props.email} />
      </div>
    </div>
  );
}

export default Card;
```
In Detail.jsx:
```
import React from "react";

function Detail(props) {
  return <p className="info">{props.detailInfo}</p>;
}

export default Detail;
```
In contacts.js:
```
const contacts = [
  {
    id: 1,
    name: "Beyonce",
    imgURL:
      "https://blackhistorywall.files.wordpress.com/2010/02/picture-device-independent-bitmap-119.jpg",
    phone: "+123 456 789",
    email: "b@beyonce.com"
  },
  {
    id: 2,
    name: "Jack Bauer",
    imgURL:
      "https://pbs.twimg.com/profile_images/625247595825246208/X3XLea04_400x400.jpg",
    phone: "+987 654 321",
    email: "jack@nowhere.com"
  },
  {
    id: 3,
    name: "Chuck Norris",
    imgURL:
      "https://i.pinimg.com/originals/e3/94/47/e39447de921955826b1e498ccf9a39af.png",
    phone: "+918 372 574",
    email: "gmail@chucknorris.com"
  }
];

export default contacts;
```
`React DevTools` can show the React DOM tree, and we can see the props being passed around to each of the components. When you click on a component in the DOM tree, you can see all the props passed into it, this is useful for `debugging`. In Chrome, add `React Developer Tools` to the extensions. Next, open Chrom Developer Tools, at the end of the tools bar, there is a `*Components` tab. On the left of the Search bar, there is an icon that allow you to select components on the webpage. This tool can also be applied to other websites such as airbnb website. 

## Mapping Data to Components
Previously in App.jsx file:
```
import React from "react";
import Card from "./Card";
import contacts from "../contacts";

function App() {
  return (
    <div>
      <h1 className="heading">My Contacts</h1>

      <Card
        name={contacts[0].name}
        img={contacts[0].imgURL}
        tel={contacts[0].phone}
        email={contacts[0].email}
      />
      <Card
        name={contacts[1].name}
        img={contacts[1].imgURL}
        tel={contacts[1].phone}
        email={contacts[1].email}
      />
      <Card
        name={contacts[2].name}
        img={contacts[2].imgURL}
        tel={contacts[2].phone}
        email={contacts[2].email}
      />
    </div>
  );
}

export default App;
```

In App.jsx file:
```
import React from "react";
import Card from "./Card";
import contacts from "../contacts";

function createCard(contact) {
  return (
    <Card
      key={contact.id}
      name={contact.name}
      img={contact.imgURL}
      tel={contact.phone}
      email={contact.email}
    />
  );
}

function App() {
  return (
    <div>
      <h1 className="heading">My Contacts</h1>
      {contacts.map(createCard)}
    </div>
  );
}

export default App;
```






























