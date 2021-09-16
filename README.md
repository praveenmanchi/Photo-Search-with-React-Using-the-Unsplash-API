# Photo-Search-with-React-Using-the-Unsplash-API
This article will discuss the step-by-step process of building a photo search application with React using the Unsplash API. Unsplash is currently one of the most used and popular photo search engines, and can be a great data provider when building projects and applications.


At the end of this tutorial, you’ll have a working application that uses React Hooks to query the Unsplash API. This project can also act as a boilerplate, since you can re-use the same programming logic and can use it as a base to build other projects involving API calls. Your photo search application will include a search bar and rendered results, as shown in the following:

   ![photo_search_application](https://user-images.githubusercontent.com/49606401/133543846-b3fc81a2-37c2-4e10-b6b3-3119d8fef91f.gif)
   

# Prerequisites


1. You will need a free Unsplash account, which you can get at the official Unsplash website.
2. You will need a development environment running Node.js; this tutorial was tested on Node.js version 10.20.1 and npm version 6.14.4
3. You will also need a basic knowledge of JavaScript and HTML, which you can find in our How To Build a Website with HTML series and in How To Code in JavaScript.   Basic knowledge of CSS would also be useful, which you can find at the Mozilla Developer Network.

# Step 1 — Creating an Empty Project

In this step, you will make use of Create React App, which will get the initial project running without doing any manual configuration. In your project directory, run the following command.

``` 
   npx create-react-app react-photo-search

```
This command will create a folder named `  react-photo-search `  with all the necessary files and configuration for a working React web aplication.

Use the `cd ` command to change directory and go inside this folder by running the following command:

``` 
   cd react-photo-search

```
Next, start the development server by running the following command:

``` 
  npm start
  
```
Next, head over to  ` http://localhost:3000 ` in a web browser, or if you are running this from a remote server, `  http://your_domain:3000 ` .

![react_starting_template](https://user-images.githubusercontent.com/49606401/133546990-b9e52a1f-3ffd-4c40-8e3f-f80dface2883.png)

Before moving further, you will have to clean the files. Create React App comes with sample code that is not needed and should be removed before building a project to ensure code maintainability.

You will now need to open another terminal since one is already taken up by ` npm start `.

Delete the default styling in ` index.css ` by running the following command:

```
rm src/index.css

```

Next, open index.js in a code editor with the following command:

```
nano src/index.js

```

Since you have deleted ` index.css. `, remove import ` './index.css'; ` from ` index.js `.

Your ` index.js ` will be similar to this once you are done removing import ` ./index.css ` from it.

### react-photo-search/src/index.js

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();

```
Save and exit the file.

Now delete the React logo by running the following command in the terminal:

```
rm src/logo.svg

```
Open ` App.css ` with the following command:

```
nano src/App.css

```
Remove everything from ` App.css,` then save and exit the file. You will update this in Step 3 with your new styling.

Open ` src/App.js ` with the following command:

```
nano src/App.js

```

The next step is to remove import logo from ` './logo.svg'; ` and remove the JSX from the ` div `with the `className="App"` in ` App.js ` file. This will remove the HTML elements of the template.

Modify `App.js` to look like this:

### react-photo-search/src/App.js

```
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">

    </div>
  );
}

export default App;

```




</code></pre>
<p>Your <code>http://localhost:3000</code> will be blank now.</p>

<p>You&rsquo;ve now initialized a React app and cleaned the sample code from it. Next, you will create a new application in the Unsplash Developer dashboard and copy the <code>Access Key</code> and <code>Secret Key</code> of the application you just created to gain access to the Unsplash API.</p>

<h2 id="step-2-—-acquiring-unsplash-api-credentials">Step 2 — Acquiring Unsplash API Credentials</h2>

<p>In this section, you will apply for an Unsplash Developer Account, create a new application for this project, and copy the <code>Access Key</code> and <code>Secret Key</code> of this application to gain access to the Unsplash API. Since the Unsplash API is not a public API, you will need your own set of Unsplash API keys for this project. </p>

<p>Head over to <a href="https://unsplash.com/developers">Unsplash Developer Home</a> and register as a developer. Since you already created an Unsplash Account this will be a quick process.</p>

<p>On the Unsplash Developer page, click the <strong>Register as a developer</strong> button.</p>

<p><img src="https://assets.digitalocean.com/articles/67359/unsplash_dev_page.png" alt="Unsplash Developer page"></p>

<p>Fill in your credentials to register.</p>

<p>After registering as a developer, you will be automatically redirected to your <a href="https://unsplash.com/oauth/applications">developer dashboard</a>. Click on <strong>New Application</strong>.</p>

<p><img src="https://assets.digitalocean.com/articles/67359/dashboard_with_new_app.png" alt="Unsplash Developer Dashboard with New Application"></p>

<p>You will be asked to accept the <strong>API Use and Guidelines</strong>. Click the checkboxes then the <strong>Accept terms</strong> button to proceed further:</p>

<p><img src="https://assets.digitalocean.com/articles/67359/api_use_guidelines.png" alt="Unsplash API Use and Guidelines"></p>

<p>You will then be prompted to give your <strong>Application information</strong>. Give your application an appropriate name and description, and click <strong>Create application</strong>. </p>

<p><img src="https://assets.digitalocean.com/articles/67359/app_info_popup.png" alt="Unsplash Application Information Pop-up"></p>

<p>With this, you have created an application and can now access your <code>Access Key</code> and <code>Secret Key</code> under the <strong>Keys</strong> section. Copy these keys to a secure location; you will need them later in your code.</p>

<p><img src="https://assets.digitalocean.com/articles/67359/keys_section.png" alt="Keys section of the Unsplash Application Page"></p>

<p>Note that you will see a <strong>Demo</strong> tag after your application name:</p>

<p><img src="https://assets.digitalocean.com/articles/67359/demo_tag.png" alt="Demottag Next To Unsplash Application Name"></p>

<p>This tag means your application is in development mode and the requests are limited to 50 per hour. For a personal project, this is more than enough, but you can also apply for production which will increase the requests limit to 5000 per hour. Do remember to follow the <a href="https://help.unsplash.com/en/articles/2511245-unsplash-api-guidelines">API Guidelines</a> before applying.</p>

<p>In this section, you created an Unsplash API application and acquired the keys required for this project. For this project, you will use the official <a href="https://github.com/unsplash/unsplash-js">Unsplash JavaScript Library</a>, <code>unsplash-js</code>, to integrate the API with your app. You will install <code>unsplash.js</code> and add CSS to style your project in the next step.</p>

<h2 id="step-3-—-installing-dependencies-and-adding-css">Step 3 — Installing Dependencies and Adding CSS</h2>

<p>You will now install the <code>unsplash-js</code> package as a dependency and add custom CSS to style your project. If at any point you get stuck, refer to the <a href="https://github.com/do-community/react-photo-search">DigitalOcean Community Repository for this project</a>.</p>

<p>To install <code>unsplash-js</code> library with the <a href="https://www.digitalocean.com/community/tutorials/how-to-use-node-js-modules-with-npm-and-package-json#step-2-%E2%80%94-installing-modules">npm package manager</a>, run the following in your project directory:</p>
<pre class="code-pre command prefixed"><code class="code-highlight language-bash"><ul class="prefixed"><li class="line" data-prefix="$">npm install unsplash-js
</li></ul></code></pre>
<p>This is the only library that you will need to install to follow this tutorial; later on, you can experiment with different React User Interface libraries like <a href="https://react-bootstrap.github.io/">React-Bootstrap</a>, <a href="https://react.semantic-ui.com/">Semantic UI React</a>, etc. You should add these libraries if, after following this tutorial, you want to tweak this project and change its layout.</p>

<p>Next, you will style your React app. Open <code>App.css</code> by running the following command.</p>
<pre class="code-pre command prefixed"><code class="code-highlight language-bash"><ul class="prefixed"><li class="line" data-prefix="$">nano src/App.css
</li></ul></code></pre>
<p>This tutorial will discuss the CSS piece by piece. </p>

<p>First is the <code>*</code> selector, which selects all the elements. Add the following code:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">* {
  box-sizing: border-box;
  background-color: rgb(244, 244, 244);
  color: #333;
  font-size: 10px;
}
</code></pre>
<p>The <code>box-sizing</code> property sets how the total width and height of an element is calculated and, in this case, it tells the browser to take border and padding into the calculation for an element&rsquo;s width and height. The background color is set using <code>background-color</code> and the value is <code>rgb(244, 244, 244)</code>, which gives a pale white color to the background. <code>color</code> sets the color of the text of the elements; here hexcode <code>#333</code> is used, which is a dark shade of gray. <code>font-size</code> sets the size of the font.</p>

<p>Next, add the <code>.App</code> block, which selects the element with the <code>className="App"</code>. By default the parent element (<code>className="App"</code>) has some margin and padding, so the following code sets <code>margin</code> and <code>padding</code> of all four sides to <code>0</code>:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">* {
  box-sizing: border-box;
  background-color: rgb(244, 244, 244);
  color: #333;
  font-size: 10px;
}

<span class="highlight">.App {</span>
  <span class="highlight">margin: 0;</span>
  <span class="highlight">padding: 0;</span>
<span class="highlight">}</span>
</code></pre>
<p>Next, add styling to the <code>div</code> element with the <code>className="container"</code>. This is the child element of the <code>div</code> with <code>className="App"</code>. Everything including title, form, button, and images will be included in this <code>div</code>:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">* {
  box-sizing: border-box;
  background-color: rgb(244, 244, 244);
  color: #333;
  font-size: 10px;
}

.App {
  margin: 0;
  padding: 0;
}

<span class="highlight">.container {</span>
  <span class="highlight">margin: 0 auto;</span>
  <span class="highlight">max-width: 1000px;</span>
  <span class="highlight">padding: 40px;</span>
<span class="highlight">}</span>
</code></pre>
<p>The <code>margin</code> property is used to defined space around elements. <code>margin</code> can be set for <code>top</code>, <code>right</code>, <code>bottom</code>, and <code>left</code>. If only one value is added, then this one value will set for all <code>top</code>, <code>right</code>, <code>bottom</code>, and <code>left</code>. If two values are added in <code>margin</code>, then the first value will be set for <code>top</code> and <code>bottom</code>, and the second will be set for <code>right</code> and <code>left</code>. </p>

<p>According to <code>margin: 0 auto;</code>, <code>top</code> and <code>bottom</code> have <code>0</code> margins while <code>left</code> and <code>right</code> have <code>auto</code>. This <code>auto</code> means that the browser will set the margin based on the container. An example to understand this will be if the parent element is <code>100px</code> and the child element is <code>50px</code>, then the <code>left</code>, and <code>right</code> margins will be <code>25px</code>, which will center the child element inside the parent element.</p>

<p><code>max-width</code> sets the maximum value of <code>width</code> of the element, which in this case is <code>1000px</code>. If the content is larger than <code>1000px</code>, then the <code>height</code> property of the element will change accordingly, else <code>max-width</code> will have no effect.</p>

<p>As discussed above, <code>margin</code> sets the space around the element while <code>padding</code> sets the space between an element and its content. The earlier code means that the <code>container</code> <code>div</code> and the elements inside it will have <code>40px</code> of space between them from all four sides.</p>

<p>Next, add styling for the title of the application:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">...
.container {
  margin: 0 auto;
  max-width: 1000px;
  padding: 40px;
}

<span class="highlight">.title {</span>
  <span class="highlight">font-size: 4.4rem;</span>
  <span class="highlight">font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;</span>
<span class="highlight">}</span>
</code></pre>
<p><code>.title</code> corresponds to the title of your App, which is &ldquo;React Photo Search&rdquo;. Only two properties are set, which are <code>font-size</code> and <code>font-family</code>. Here, the <code>rem</code> unit is used for the <code>font-size</code> value. <code>rem</code> values are relative to the root <code>html</code> element, unlike <code>em</code> values, which are relative to the parent element. Here the <code>4.4rem</code> means <code>44px</code> (4.4 x 10). This multiplication by <code>10px</code> is because you set the font size of all elements to <code>10px</code> using <code>*</code> selector. <code>font-family</code> specifies the font of the element. There are many values passed in the code to act as a <em>fallback</em> system; if the browser does not provide the first font, the next font is set.</p>

<p>Next is the <code>.form</code> CSS block, which includes the form that will be used to search for images. This includes the input search field, button, and label.</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">...
.title {
  font-size: 4.4rem;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}

<span class="highlight">.form {</span>
  <span class="highlight">display: grid;</span>
<span class="highlight">}</span>
</code></pre>
<p>Here, only the <code>display</code> property is set. This property specifies the display behavior of the element. It can take different values like <code>grid</code>, <code>flex</code>, <code>block</code>, <code>inline</code>, etc. <code>grid</code> displays an element as a block-level and renders the content according to the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/grid">grid model</a>.</p>

<p>Next is the <code>.label</code> and the <code>.input</code> CSS block:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">...
.form {
  display: grid;
}

<span class="highlight">.label {</span>
  <span class="highlight">font-size: 3rem;</span>
  <span class="highlight">margin-bottom: 1rem;</span>
<span class="highlight">}</span>

<span class="highlight">.input {</span>
  <span class="highlight">font-size: 1.6rem;</span>
  <span class="highlight">padding: 0.5rem 2rem;</span>
  <span class="highlight">line-height: 2.8rem;</span>
  <span class="highlight">border-radius: 20px;</span>
  <span class="highlight">background-color: white;</span>
  <span class="highlight">margin-bottom: 1rem;</span>
<span class="highlight">}</span>
</code></pre>
<p>We have already discussed <code>font-size</code>, <code>padding</code>, <code>background-color</code>, and <code>margin-bottom</code>, so let&rsquo;s discuss <code>line-height</code> and <code>border-radius</code>. <code>border-radius</code> defines the radius of the element&rsquo;s corners. Here the value is set to <code>20px</code>, which will be used for all the four sides. Setting <code>border-radius</code> to <code>50%</code> can make a square element into an oval. <code>line-height</code> specified the height of the line, which is set to <code>2.8rem</code> or <code>28px</code>. </p>

<p>Next is the <code>.button</code> CSS block, which styles the <strong>Search</strong> button:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">...
.input {
  font-size: 1.6rem;
  padding: 0.5rem 2rem;
  line-height: 2.8rem;
  border-radius: 20px;
  background-color: white;
  margin-bottom: 1rem;
}

<span class="highlight">.button {</span>
  <span class="highlight">background-color: rgba(0, 0, 0, 0.75);</span>
  <span class="highlight">color: white;</span>
  <span class="highlight">padding: 1rem 2rem;</span>
  <span class="highlight">border: 1px solid rgba(0, 0, 0, 0.75);</span>
  <span class="highlight">border-radius: 20px;</span>
  <span class="highlight">font-size: 1.4rem;</span>
  <span class="highlight">cursor: pointer;</span>
  <span class="highlight">transition: background-color 250ms;</span>
<span class="highlight">}</span>
</code></pre>
<p>We have already discussed <code>background-color</code>, <code>color</code>, <code>padding</code>, <code>border-radius</code>, and <code>font-size</code>. <code>border</code> sets the style, width, and color of the border of an element. Here <code>border</code> is used as a shorthand property for <code>border-width</code>, <code>border-style</code>, and <code>border-color</code>. This code adds a solid black color border of 1px around the <strong>Search</strong> button. <code>cursor</code> specifies the mouse cursor when pointing over an element. </p>

<p>Next is the <code>:hover</code> selector, which is used on <code>.button</code>. </p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">...
.button {
  background-color: rgba(0, 0, 0, 0.75);
  color: white;
  padding: 1rem 2rem;
  border: 1px solid rgba(0, 0, 0, 0.75);
  border-radius: 20px;
  font-size: 1.4rem;
  cursor: pointer;
  transition: background-color 250ms;
}

<span class="highlight">.button:hover {</span>
  <span class="highlight">background-color: rgba(0, 0, 0, 0.85);</span>
<span class="highlight">}</span>
</code></pre>
<p>This means that when the mouse is hovered over the <code>.button</code> element, the background color will change.</p>

<p>The next CSS block is <code>.card-list</code>, which corresponds to the <code>div</code> with <code>className="card-list"</code>. This <code>div</code> will display all the images inside it:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">...
.button:hover {
  background-color: rgba(0, 0, 0, 0.85);
}

<span class="highlight">.card-list {</span>
  <span class="highlight">column-count: 3;</span>
<span class="highlight">}</span>
</code></pre>
<p><code>column-count</code> divides the element into columns according to the value that is passed inside it. This code will divide the <code>card-list</code> <code>div</code> into three columns, and the images will be displayed within these three columns.</p>

<p>Next are the <code>.card</code> and <code>.card--image</code> CSS blocks. <code>.card</code> refers to the individual <code>div</code> with an image inside it, and <code>.card--image</code> is the <code>className</code> of this image:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">...
.card-list {
  column-count: 3;
}

<span class="highlight">.card {</span>
    <span class="highlight">margin-bottom: 1rem;</span>
    <span class="highlight">display: flex;</span>
<span class="highlight">}</span>

<span class="highlight">.card--image {</span>
    <span class="highlight">flex: 100%;</span>
    <span class="highlight">margin-top: 1rem;</span>
    <span class="highlight">border-radius: 10px;</span>
<span class="highlight">}</span>
</code></pre>
<p>We have already discussed <code>margin</code>, <code>display</code>, and <code>border-radius</code>. In <code>.card</code>, <code>display</code> is set to <code>flex</code>, which means the elements will behave like block elements, and the display will be set according to the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout">flexbox model</a>. By using the shorthand property <code>flex:100%;</code>, you set the value for <code>flex-grow</code>, <code>flex-shrink</code>, and <code>flex-basis</code>. You can read more about it <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/flex">at the Mozilla Developer Network</a>.</p>

<p>The final CSS blocks involve <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries">media queries</a>. By using the <code>@media</code> rule, you can apply different styles for different media types/devices:</p>
<div class="code-label " title="react-photo-search/src/App.css">react-photo-search/src/App.css</div><pre class="code-pre "><code class="code-highlight language-css">...
.card--image {
    flex: 100%;
    margin-top: 1rem;
    border-radius: 10px;
}

<span class="highlight">@media (min-width: 768px) {</span>
  <span class="highlight">.form {</span>
    <span class="highlight">grid-template-columns: auto 1fr auto;</span>
    <span class="highlight">grid-gap: 1rem;</span>
    <span class="highlight">align-items: center;</span>
  <span class="highlight">}</span>
  <span class="highlight">.input {</span>
    <span class="highlight">margin-bottom: 0;</span>
  <span class="highlight">}</span>
<span class="highlight">}</span>

<span class="highlight">@media only screen and (max-width: 600px) {</span>
    <span class="highlight">.card-list {</span>
        <span class="highlight">column-count: 1;</span>
    <span class="highlight">}</span>
<span class="highlight">}</span>
</code></pre>
<p>According to this code, <code>column-count</code> will change from <code>3</code> to <code>1</code> when the browser window is <code>600px</code> or less (applicable for most mobile devices). This used the <code>max-width</code> property with the <code>@media</code> rule. The code before that uses <code>min-width</code>, which changes the style of the elements inside the <code>@media</code> rule when the width is <code>768px</code> or more.</p>

<p><code>grid-template-columns</code> is used to specify columns in the grid model. The number of columns is equal to the number of values passed, which is three according to the code (<code>auto 1fr auto</code>). The first and third grid element&rsquo;s size will be according to their container size or the content&rsquo;s size. The second element will be given <code>1fr</code> (Fractional Unit), or the space left after the first and third elements have occupied according to their size. These three elements will be a camera emoji, the search input field, and the <strong>Search</strong> button. After the emoji and the button have taken the space according to their size, the rest of the area will go to the search input field, and it will change its width accordingly.</p>

<p><code>grid-gap: 1rem;</code> creates a space of <code>1rem</code> between two grid lines. <code>align-items:center;</code> positions the items in the center of the container.</p>

<p>This finishes the styling of your application. Save and exit from <code>src/App.css</code>. If you&rsquo;d like to see the whole CSS file together, take a look at the <a href="https://github.com/do-community/react-photo-search/blob/master/src/App.css">GitHub repository for this code</a>.</p>

<p>Now that you have installed the necessary dependency and added the custom CSS needed to style your project, you can move forward to the next section and design the UI or layout of the project.</p>

<h2 id="step-4-—-designing-the-user-interface">Step 4 — Designing the User Interface</h2>

<p>In this section, you will design the UI of the project. This will include elements like a heading, label, input field, and button.</p>

<p>Open the <code>src/App.js</code> file with the following command:</p>
<pre class="code-pre command prefixed"><code class="code-highlight language-bash"><ul class="prefixed"><li class="line" data-prefix="$">nano src/App.js
</li></ul></code></pre>
<p>To add a heading to your project, create a <code>div</code> with the <code>className="container"</code> inside your <code>App.js</code>. Inside this <code>div</code> add an <code>h1</code> tag with the <code>className="title"</code> and write <code>React Photo Search</code> inside the tag. This will be the title heading: </p>
<div class="code-label " title="react-photo-search/src/App.js">react-photo-search/src/App.js</div><pre class="code-pre "><code class="code-highlight language-javascript">import React from 'react';
import './App.css';

function App() {
  return (
    &lt;div className="App"&gt;
      <span class="highlight">&lt;div className="container"&gt;</span>
        <span class="highlight">&lt;h1 className="title"&gt;React Photo Search&lt;/h1&gt;</span>
      <span class="highlight">&lt;/div&gt;</span>
    &lt;/div&gt;
  );
}
</code></pre>
<p>Save and exit the file. In your browser, your app will now show your title: </p>

<p><img src="https://assets.digitalocean.com/articles/67359/app_with_title.png" alt='Application with "React Photo Search" Title'></p>

<p>Next, you will create a form that will take input from the user. This form will consist of an input text field and a submit button. </p>

<p>For this, create a new <a href="https://www.digitalocean.com/community/tutorials/how-to-create-custom-components-in-react">component</a> named <code>&lt;SearchPhotos /&gt;</code>. It is not necessary to create a separate component, but as you develop this project, splitting code into components makes it easier to write and maintain code.</p>

<p>In the <code>src</code> folder, create and open a new file called <code>searchPhotos.js</code> with the following command:</p>
<pre class="code-pre command prefixed"><code class="code-highlight language-bash"><ul class="prefixed"><li class="line" data-prefix="$">nano src/searchPhotos.js
</li></ul></code></pre>
<p>Inside <code>searchPhotos.js</code>, you export a functional component named <code>&lt;SearchPhotos /&gt;</code>:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">import React from "react";

export default function SearchPhotos() {
  return (
    &lt;&gt;

    &lt;/&gt;
  );
}
</code></pre>
<p>This is the basic structure of a functional component that you need to add to the <code>searchPhotos.js</code>file. Save this file.</p>

<p>The next step is to import and use the <code>SearchPhotos</code> component in <code>App.js</code>.</p>

<p>In a new terminal window, open up <code>App.js</code>:</p>
<pre class="code-pre command prefixed"><code class="code-highlight language-bash"><ul class="prefixed"><li class="line" data-prefix="$">nano src/App.js
</li></ul></code></pre>
<p>Add the following highlighted lines to <code>App.js</code>:</p>
<div class="code-label " title="react-photo-search/src/App.js">react-photo-search/src/App.js</div><pre class="code-pre "><code class="code-highlight language-javascript">import React from "react";
import "./App.css";
<span class="highlight">import SearchPhotos from "./searchPhotos"</span>

function App() {
  return (
    &lt;div className="App"&gt;
      &lt;div className="container"&gt;
        &lt;h1 className="title"&gt;React Photo Search&lt;/h1&gt;
        <span class="highlight">&lt;SearchPhotos /&gt;</span>

      &lt;/div&gt;
    &lt;/div&gt;
  );
}
export default App;
</code></pre>
<p>Save this file.</p>

<p>To create the search form, you will use the <code>form</code> tag and inside it, create an input field using the <code>input</code> tag and a button using the <code>button</code> tag. </p>

<p>Give the elements the <code>className</code> of their respective tags. While you are doing this, add a label with a camera emoji inside it for styling:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
export default function SearchPhotos() {
  return (
    &lt;&gt;
      <span class="highlight">&lt;form className="form"&gt; </span>
        <span class="highlight">&lt;label className="label" htmlFor="query"&gt; </span>
          <span class="highlight">{" "}</span>
          <span class="highlight">📷</span>
        <span class="highlight">&lt;/label&gt;</span>
        <span class="highlight">&lt;input</span>
          <span class="highlight">type="text"</span>
          <span class="highlight">name="query"</span>
          <span class="highlight">className="input"</span>
          <span class="highlight">placeholder={`Try "dog" or "apple"`}</span>
        <span class="highlight">/&gt;</span>
        <span class="highlight">&lt;button type="submit" className="button"&gt;</span>
          <span class="highlight">Search</span>
        <span class="highlight">&lt;/button&gt;</span>
      <span class="highlight">&lt;/form&gt;</span>
    &lt;/&gt;
  );
}
</code></pre>
<p>First, you created a <code>form</code> element with a <code>className="form"</code>, and inside it a <code>label</code> with a camera emoji. Then comes the <code>input</code> element with attributes <code>type="text"</code>, since the search query will be a <a href="https://www.digitalocean.com/community/tutorials/how-to-work-with-strings-in-javascript">string</a>. The <code>name="query"</code> attribute specifies the name of the <code>input</code> element, <code>className="input"</code> gives the element a class for styling, and the placeholder value for the search bar is set to <code>Try "dog" or "apple"</code>. The final element in <code>form</code> is a <code>button</code> with the <code>type="submit"</code>.</p>

<p>Save and exit the file. Your app will now have a search bar after the title:</p>

<p><img src="https://assets.digitalocean.com/articles/67359/app_with_search_bar.png" alt="Application with search bar and placeholder text of 'Try &quot;dog&quot; or &quot;apple&quot;'"></p>

<p>Now that the UI of the app is complete, you can start working on the functionalities by first storing the input query from the user in the next section.</p>

<h2 id="step-5-—-setting-state-using-search-query">Step 5 — Setting State Using Search Query</h2>

<p>In this step, you will learn about <a href="https://www.digitalocean.com/community/tutorials/how-to-manage-state-on-react-class-components">states</a> and <a href="https://www.digitalocean.com/community/tutorials/how-to-manage-state-with-hooks-on-react-components">React Hooks</a> and then use them to store user input.</p>

<p>Now that you have constructed your application&rsquo;s basic structure, we can discuss the React side of things. You have a form, but it doesn’t do anything yet, so the first thing to do is to take the input from the search bar and access it. You can do this with states.</p>

<p>States at their core are <a href="https://www.digitalocean.com/community/tutorials/understanding-objects-in-javascript">objects</a> that are used to store the property values of components. Every time the state changes, the component re-renders. For this app, you need a state that will store the input or query from the search bar whenever the <strong>Search</strong> button is clicked.</p>

<p>One of the things that you may have noticed is that this project is using functional components. This allows you to use React Hooks to manage state. Hooks are functions that use React features like defining a state without writing a class. In this tutorial, you will make use of the <code>useState()</code> Hook.</p>

<p>The first thing to do is import <code>useState</code> inside your <code>searchPhotos.js</code> file. </p>

<p>Open up the file:</p>
<pre class="code-pre command prefixed"><code class="code-highlight language-bash"><ul class="prefixed"><li class="line" data-prefix="$">nano src/searchPhotos.js
</li></ul></code></pre>
<p>Modify the first line of <code>searchPhotos.js</code> file to the following:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">import React<span class="highlight">, { useState }</span> from "react";

export default function SearchPhotos() {
...
</code></pre>
<p>Next, you will implement <code>useState()</code>. This is the syntax for the <code>useState()</code> Hook:</p>
<pre class="code-pre "><code class="code-highlight language-javascript">useState(<span class="highlight">initialState</span>)
</code></pre>
<p><code>useState()</code> returns the current state and a function commonly known as an updater function. To store these, you can use <a href="https://www.digitalocean.com/community/tutorials/understanding-destructuring-rest-parameters-and-spread-syntax-in-javascript#destructuring">array destructuring</a>:</p>
<pre class="code-pre "><code class="code-highlight language-javascript">const [query, setQuery] = useState(<span class="highlight">initialState</span>);
</code></pre>
<p>In this example, <code>query</code> stores the current state of the component, and <code>setQuery</code> is a function that can be called to update the state. <code>initialState</code> defines the initial state value; it can be a string, a number, an array, or an object depending on the use.</p>

<p>In your project, the input from the search bar is a string, so you will use an empty string as an initial value of the state.</p>

<p>In your <code>searchPhotos.js</code> file, add the following line of code:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...

export default function SearchPhotos() {
  <span class="highlight">const [query, setQuery] = useState("");</span>

  return (
    &lt;&gt;
      &lt;form className="form"&gt;
        &lt;label className="label" htmlFor="query"&gt;
          {" "}
          📷
        &lt;/label&gt;
...
</code></pre>
<p>The next step is to set the <code>value</code> of the input text field to <code>query</code> and add an <code>onChange()</code> event to it. This <code>onChange()</code> event will have a function, inside which <code>setQuery()</code> will be used to update the state. The input string is retrieved using <a href="https://www.digitalocean.com/community/tutorials/understanding-events-in-javascript#event-objects"><code>e.target.value</code></a>:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
&lt;input
    type="text"
    name="query"
    className="input"
    placeholder={`Try "dog" or "apple"`}
    <span class="highlight">value={query}</span>
    <span class="highlight">onChange={(e) =&gt; setQuery(e.target.value)}</span>
/&gt;
...
</code></pre>
<p>Now, the state and the input field&rsquo;s values are interlinked, and you can use this search query to search for the image.</p>

<p>You can view the input from the search bar inside the <code>query</code> in real-time for testing purposes. Add <code>console.log(query)</code> just after where you defined state:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
export default function SearchPhotos() {
   const [query, setQuery] = useState("");
   <span class="highlight">console.log(query);</span>

  return (
    &lt;&gt;
    //
    &lt;/&gt;
  );
}

</code></pre>
<p>Save the file.</p>

<p>You will now receive the input queries inside the console. You can open your console, using <code>F12</code> in <a href="https://www.google.com/chrome/">Chrome</a> or <code>Ctrl+Shift+K</code> in <a href="https://www.mozilla.org/en-US/firefox/">Firefox</a>:</p>

<p><img src="https://assets.digitalocean.com/articles/67359/console_logging_input.png" alt="Browser console demonstrating the logging of the user input for this application."></p>

<p>Now, <code>searchPhotos.js</code> will look like this:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">
import React, { useState } from "react";
export default function SearchPhotos() {
  const [query, setQuery] = useState("");
  console.log(query);

  return (
    &lt;&gt;
      &lt;form className="form"&gt;
        &lt;label className="label" htmlFor="query"&gt;
          {" "}
          📷
        &lt;/label&gt;
        &lt;input
          type="text"
          name="query"
          className="input"
          placeholder={`Try "dog" or "apple"`}
          value={query}
          onChange={(e) =&gt; setQuery(e.target.value)}
        /&gt;
        &lt;button type="submit" className="button"&gt;
          Search
        &lt;/button&gt;
      &lt;/form&gt;
    &lt;/&gt;
  );
}
</code></pre>
<p>This section discussed states and React Hooks and stored the user input in the <code>input</code> field inside the <code>query</code> state. In the next section, you will use this search query to search for the image and store the response inside another state.</p>

<h2 id="step-6-—-making-api-requests-to-unsplash">Step 6 — Making API Requests to Unsplash</h2>

<p>You will now use the <code>unsplash-js</code> library to search for images using the query from the <code>input</code> field. The response will be stored inside another state named <code>pics</code>.</p>

<p>You have already installed the <code>unsplash-js</code> library, so import it in <code>searchPhotos.js</code> file. You can also remove the <code>console.log()</code> statement from the previous section:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">import React, { useState } from "react";
<span class="highlight">import Unsplash, { toJson } from "unsplash-js";</span>

...
</code></pre>
<p><code>toJson</code> is a helper function in the <code>unsplash-js</code> library that is used to convert the response into <a href="https://www.digitalocean.com/community/tutorials/how-to-work-with-json-in-javascript">JSON format</a>. You can learn more about helper functions at the <a href="https://github.com/unsplash/unsplash-js#helpers"><code>unsplash-js</code> GitHub page</a>.</p>

<p>To use Unsplash in your app, make an instance of it using the <code>new</code>  keyword like this:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">import React, { useState } from "react";
import Unsplash, { toJson } from "unsplash-js";

<span class="highlight">const unsplash = new Unsplash({</span>
  <span class="highlight">accessKey: "your_Access_Key",</span>
<span class="highlight">});</span>
</code></pre>
<p>Paste your Unsplash <code>Access Key</code> to replace <code><span class="highlight">your_Access_Key</span></code> and you can now make API requests. </p>

<p><span class='warning'><strong>Warning:</strong> One should never share any access keys or Client ID&rsquo;s for an API or any service. Potential bad actors can misuse them over the internet. In this scenario, they can make an unusual amount of requests that can be flagged as spam by your service provider, which can deactivate your application and account.<br></span></p>

<p>Now you will create an <a href="https://www.digitalocean.com/community/tutorials/understanding-the-event-loop-callbacks-promises-and-async-await-in-javascript">asynchronous function</a> that will be triggered when clicking the <strong>Search</strong> button.</p>

<p>Just after where you defined state for <code>query</code>, define an <code>async</code> function:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
export default function SearchPhotos() {
  const [query, setQuery] = useState("");

  <span class="highlight">const searchPhotos = async (e) =&gt; {</span>
    <span class="highlight">e.preventDefault();</span>
    <span class="highlight">console.log("Submitting the Form")</span>
  <span class="highlight">};</span>
</code></pre>
<p>Here <code>e.preventDefault()</code> stops the page from reloading whenever the <strong>Search</strong> button is clicked. You can pass this function in the <code>onSubmit</code> event inside the <code>form</code> tag. You can read more about this in the <a href="https://reactjs.org/docs/forms.html">official React docs</a>.</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
  return (
    &lt;&gt;
      &lt;form className="form" <span class="highlight">onSubmit={searchPhotos}</span>&gt;
...
</code></pre>
<p>Save the file. Now, if you click the <strong>Search</strong> button, you will receive <code>Submitting the Form</code> in the console. You can remove this <code>console.log()</code> after a successful response in the console.</p>

<p>Inside your <code>searchPhotos()</code> function, you will use the Unsplash instance (<code>unsplash</code>). You can use the <code>search</code> method for searching the images. Here is the syntax for that:</p>
<pre class="code-pre "><code class="code-highlight language-javascript">search.photos(<span class="highlight">keyword</span>, <span class="highlight">page</span>, <span class="highlight">per_page</span>, <span class="highlight">filters</span>)
</code></pre>
<p>Here is the code to search for an image; add this code inside your <code>searchPhotos()</code> function:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
const searchPhotos = async (e) =&gt; {
  e.preventDefault();
  <span class="highlight">unsplash.search</span>
    <span class="highlight">.photos(query)</span>
    <span class="highlight">.then(toJson)</span>
    <span class="highlight">.then((json) =&gt; {</span>
      <span class="highlight">console.log(json);</span>
    <span class="highlight">});</span>
};
...
</code></pre>
<p>First, you use <code>unsplash.search</code> and then specify what to search for, which is in this case <code>photos</code>. We can also search for <code>users</code> or <code>collections</code>. <code>photos</code> takes the first required argument as the keyword to search for, which is <code>query</code>; you can also specify the page, responses per page, image orientation, etc., through the optional arguments. For this tutorial, you only need the <code>page</code> and <code>per_page</code> arguments, limiting the response items you get from Unsplash.</p>

<p>Here are all the arguments that can be provided in <code>photos</code></p>

<table><thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Opt/Required</th>
<th>Default</th>
</tr>
</thead><tbody>
<tr>
<td><code>keyword</code></td>
<td>string</td>
<td>Required</td>
<td></td>
</tr>
<tr>
<td><code>page</code></td>
<td>number</td>
<td>Optional</td>
<td></td>
</tr>
<tr>
<td><code>per_page</code></td>
<td>number</td>
<td>Optional</td>
<td>10</td>
</tr>
<tr>
<td><code>filters</code></td>
<td>object</td>
<td>Optional</td>
<td></td>
</tr>
<tr>
<td><code>filters.orientation</code></td>
<td>string</td>
<td>Optional</td>
<td></td>
</tr>
<tr>
<td><code>filters.collections</code></td>
<td>array</td>
<td>Optional</td>
<td></td>
</tr>
</tbody></table>

<p>You can learn more about them at the <a href="https://github.com/unsplash/unsplash-js#search"><code>unsplash-js</code> GitHub page</a>.</p>

<p>You use the <code>toJson</code> method to convert the response into JSON, and finally, <code>console.log()</code> the response to test that API requests are made without any error. You will remove this <code>console .log ()</code> in the next steps.</p>

<p>Save the file. Now open your console and click the <strong>Search</strong> button. You will find a response JSON like this:</p>
<pre class="code-pre "><code class="code-highlight language-json">{
  "results": [{
     "description": "Pink Wall Full of Dogs",
     "alt_description": "litter of dogs fall in line beside wall",
     <span class="highlight">"urls"</span>: {
           <span class="highlight">"raw": "https://images.unsplash.com/photo-1529472119196-cb724127a98e?ixlib=rb-1.2.1&amp;ixid=eyJhcHBfaWQiOjE0MTQxN30"</span>,
           <span class="highlight">"full": "https://images.unsplash.com/photo-1529472119196-cb724127a98e?ixlib=rb-1.2.1&amp;q=85&amp;fm=jpg&amp;crop=entropy&amp;cs=srgb&amp;ixid=eyJhcHBfaWQiOjE0MTQxN30"</span>,
           <span class="highlight">"regular": "https://images.unsplash.com/photo-1529472119196-cb724127a98e?ixlib=rb-1.2.1&amp;q=80&amp;fm=jpg&amp;crop=entropy&amp;cs=tinysrgb&amp;w=1080&amp;fit=max&amp;ixid=eyJhcHBfaWQiOjE0MTQxN30"</span>,
           <span class="highlight">"small": "https://images.unsplash.com/photo-1529472119196-cb724127a98e?ixlib=rb-1.2.1&amp;q=80&amp;fm=jpg&amp;crop=entropy&amp;cs=tinysrgb&amp;w=400&amp;fit=max&amp;ixid=eyJhcHBfaWQiOjE0MTQxN30"</span>,
           <span class="highlight">"thumb": "https://images.unsplash.com/photo-1529472119196-cb724127a98e?ixlib=rb-1.2.1&amp;q=80&amp;fm=jpg&amp;crop=entropy&amp;cs=tinysrgb&amp;w=200&amp;fit=max&amp;ixid=eyJhcHBfaWQiOjE0MTQxN30</span>"
                },
    ...
}
</code></pre>
<p>You can remove or comment the <code>console.log()</code> statement when you find a successful response from the Unsplash API, which means your code is working fine. This app will use the <code>"urls"</code> field, since that will be the source of the image. </p>

<p>You&rsquo;ve now used the query from the user to search for images when the <strong>Search</strong> button was clicked using the <code>unsplash-js</code> library. Next, you will store the response inside another state named <code>pics</code> and display the images by mapping the elements inside this state.</p>

<h2 id="step-7-—-displaying-images-on-the-webpage">Step 7 — Displaying Images on the Webpage</h2>

<p>In this last section, you will store the response from Unsplash API inside another state named <code>pics</code> and then map over the elements of this state to display the images on the webpage.</p>

<p>To show images, you need to access the response JSON, and for that, another state will be needed. The previous state <code>query</code> stored queries from the user, which was used to make requests to the Unsplash API. This state <code>pics</code> will store the image response you get from Unsplash API.</p>

<p>In <code>searchPhotos.js</code> define another state like this:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
  const [query, setQuery] = useState("");
  <span class="highlight">const [pics, setPics] = useState([]);</span>
...
</code></pre>
<p>This state has been initialized with an empty <a href="https://www.digitalocean.com/community/tutorials/understanding-arrays-in-javascript">array</a>, and all the responses will be stored as an object inside this state. In other words, this is an array of objects.</p>

<p>To update this state with the JSON, you will use <code>setPics</code> inside <code>unsplash</code> API request:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
    unsplash.search
      .photos(query, 1, 20)
      .then(toJson)
      .then((json) =&gt; {
        <span class="highlight">setPics(json.results);</span>
  });
...
</code></pre>
<p>Now every time you search for a new query, this state will be updated accordingly. </p>

<p>Next, create a <code>div</code> with the <code>className="card-list"</code> just after where <code>form</code> tags end:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
        &lt;button type="submit" className="button"&gt;
          Search
        &lt;/button&gt;
      &lt;/form&gt;
      <span class="highlight">&lt;div className="card-list"&gt;</span>
      <span class="highlight">&lt;/div&gt;</span>
    &lt;/&gt;
  );
}
</code></pre>
<p>Inside this <code>div</code>, you will map through the state and display the <code>id</code> of the image:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
        &lt;button type="submit" className="button"&gt;
          Search
        &lt;/button&gt;
      &lt;/form&gt;
      &lt;div className="card-list"&gt;
        <span class="highlight">{pics.map((pic) =&gt; pic.id )}</span>
      &lt;/div&gt;
    &lt;/&gt;
  );
}
</code></pre>
<p>You first use <code>{}</code> to pass the JavaScript expression, inside which you use the <a href="https://www.digitalocean.com/community/tutorials/how-to-use-array-methods-in-javascript-iteration-methods#map()"><code>.map()</code> method</a> on your state. </p>

<p>Save your file. If you search now, you will see <code>id</code>s associated with different objects on the webpage:</p>

<p><img src="https://assets.digitalocean.com/articles/67359/app_with_overlapping_id.png" alt="Application with overlapping ID results rendered on the webpage"></p>

<p>This is messy, but this also means your application is working.</p>

<p>Instead of displaying <code>pic.id</code>, open up JSX inside the <code>map</code> function and create a new <code>div</code> with the <code>className="card"</code>. This is going to be the container for each individual image:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
        &lt;button type="submit" className="button"&gt;
          Search
        &lt;/button&gt;
      &lt;/form&gt;
      &lt;div className="card-list"&gt;
        {
          pics.map((pic) =&gt; <span class="highlight">&lt;div className="card"&gt;&lt;/div&gt;</span>);
        }
      &lt;/div&gt;
    &lt;/&gt;
  );
}
</code></pre>
<p>You can now display an image inside this <code>div</code>:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
        &lt;button type="submit" className="button"&gt;
          Search
        &lt;/button&gt;
      &lt;/form&gt;
      &lt;div className="card-list"&gt;
        {
          pics.map((pic) =&gt; 
            &lt;div className="card"&gt;
              <span class="highlight">&lt;img</span>
                <span class="highlight">className="card--image"</span>
                <span class="highlight">alt={pic.alt_description}</span>
                <span class="highlight">src={pic.urls.full}</span>
                <span class="highlight">width="50%"</span>
                <span class="highlight">height="50%"</span>
              <span class="highlight">&gt;&lt;/img&gt;</span>
            &lt;/div&gt;);
        }
      &lt;/div&gt;
    &lt;/&gt;
  );
}
</code></pre>
<p>If you go back and see the response JSON, you will find a different kind of information. <code>"urls"</code> contains the path to the image, so here <code>pic.urls.full</code> is the actual path to the image and <code>pic.alt_description</code> is the alt description of the picture. </p>

<p>There are different fields inside <code>"urls"</code> that give different data, such as:</p>

<p><code>raw</code> : Actual raw image taken by a user.<br>
<code>full</code> : Raw image in <code>.jpg</code> format.<br>
<code>regular</code> : Best for practical uses, <code>width=1080px</code>.<br>
<code>small</code> : Perfect for slow internet speed, <code>width=400px</code>.<br>
<code>thumb</code> : Thumbnail version of the image, <code>width=200px</code>.</p>

<p>In this tutorial, you are using <code>full</code>, but you can experiment with other types, too. You have also given a default <code>height</code> and <code>width</code> to the image.</p>

<p>Save your file.</p>

<p>Your application is almost finished; if you search now, you will be able to see your application in action. But there is still a small line of code left. If you search for your image and go to your console in the browser, you will see a warning.</p>
<pre class="code-pre "><code><div class="secondary-code-label " title="Web console">Web console</div>Warning: Each child in a list should have a unique "key" prop.
</code></pre>
<p>To fix this, pass a unique <code>key</code> to every child using the <code>id</code> of the image. This <code>key</code> <a href="https://www.digitalocean.com/community/tutorials/how-to-customize-react-components-with-props">prop</a> explicitly tells React the identity of each child in a list; this also prevents children from losing state between renders:</p>
<div class="code-label " title="react-photo-search/src/searchPhotos.js">react-photo-search/src/searchPhotos.js</div><pre class="code-pre "><code class="code-highlight language-javascript">...
      &lt;div className="card-list"&gt;
        {pics.map((pic) =&gt;
          &lt;div className="card" <span class="highlight">key={pic.id}</span>&gt;
            &lt;img
              className="card--image"
              alt={pic.alt_description}
              src={pic.urls.full}
              width="50%"
              height="50%"
            &gt;&lt;/img&gt;
          &lt;/div&gt;)};
      &lt;/div&gt;
    &lt;/&gt;
  );
}
</code></pre>
<p>You can adjust the number of images you want to show by passing the corresponding argument to <code>unsplash.search.photos()</code>.</p>

<p>Save and exit the file. You&rsquo;ll now have a working photo search app:</p>

<p><img src="https://assets.digitalocean.com/articles/67359/photo_search_application.gif" alt='Animation of searching the term "apple" in the application and getting image results of apples'></p>

<p>In this section, you stored the response from Unsplash API inside the <code>pics</code> state and displayed the images by mapping over the elements in <code>pics</code>.</p>

<h2 id="conclusion">Conclusion</h2>

<p>In this tutorial, you developed a React Photo Search app with the Unsplash API. In building the project, the tutorial discussed how to use React Hooks, query an API, and style a user interface.</p>



</div>




