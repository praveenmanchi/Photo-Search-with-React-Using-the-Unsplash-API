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




