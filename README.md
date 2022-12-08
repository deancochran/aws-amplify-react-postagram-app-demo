# AWS-Amplify-React-postagram-demo


This repository is a demonstration of a default react app, that is configured to be hosted on aws amplify 

- the instructions for how this repo was made can be found on the aws workshops website
  - https://catalog.us-east-1.prod.workshops.aws/workshops/9586a55a-1f61-456c-ace9-b24f505d44a4/en-US

I followed the instructions there and will not update this repo afterwards.

The core focus of this application is to utilize aws to implement a photo sharing app. Technical topics include:
- GraphQL API with AWS AppSync
- Authentication
- Object (image) storage
- Authorization
- Hosting

The Amplify CLI allows us to create a hostable application in seconds. Using the React and Node template we can launch a default app through the cli.
# Init React App
npx create-react-app postagram

<!-- Load your dependencies -->
npm install aws-amplify @emotion/css uuid react-router-dom@5 @aws-amplify/ui-react

# Deploy to Amplify

- run 'amplify configure'
  - use non root user access keys and credentials to create a amplify account
- run 'amplify init'
  - name your project and configure it accordingly
- run 'amplify console' to see your app in the aws amplify GUI 

# Attach an API
- run 'amplify add api'
  - attach a graphQL api (single object with fields)
  - you need to configure the graph api according to the documentation on the workshop
  - once configured...
- run 'amplify push'
  - this builds a local api for you and compiles the operations inside the src/ folder
- follow the docs to properly finish this section

# Test the API

To test it out we can use the GraphiQL editor in the AppSync dashboard. To open the AppSync dashboard, run the following command
- run 'amplify console api'

For this section you will want to follow the documentation on the aws workshop
- you will use AWS AppSync
  - add queries and mutations to test the api

# Now, our API is created & we can test it out in our app!
The first thing we need to do is to configure our React application to be aware of our Amplify project. We can do this by referencing the auto-generated aws-exports.js file that is now in our src folder.

add this to the src/index.js

  ```
  import Amplify from 'aws-amplify'
  import config from './aws-exports'
  Amplify.configure(config)
  ```

Now, our app is ready to start using our AWS services.
- after following the documentation, you can edit the src/ folder to display 'Hello World!' as well as some previous posts that were posted through Data Sync ealier

# Adding Authentication

- similar to adding an api, we can add an authentication mechanism with:
  - 'amplify add auth'
  - then 'amplify push' to sync the changes in the cloud

Again, the documentation provides a lot of code and resources to build the functionality of the app
- the keep features that are added in this section prevent unauthenticated users from accessing the website
- you can have users sign in with their email which allows them to access the content (content barrier)
- the documentation also allows you to add a sign in and sign out button

# Image storage with Amazon S3.

To add image storage, we'll use Amazon S3, which can be configured and created via the Amplify CLI:
- run 'amplify add storage'
- configure the storage and run 'amplify push'
  - make sure you follow the docs

Once these steps are put into place, we can use the newly created s3 bucket to import the photos into the application

save to a bucket with

  ```
  const file = e.target.files[0];
  await Storage.put(file.name, file);
  ```

retieve data from a bucket with

  ```
  const image = await Storage.get('my-image-key.jpg')
  ```
# Now you can build our your React Application
Follow the docs! copy code if needed

# Add functionality to your graph ql api with 
- amplify update api
- then follow the instructions to add more fine tuned permissions for api and cognito users
# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

### `npm test`

Launches the test runner in the interactive watch mode.
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.
