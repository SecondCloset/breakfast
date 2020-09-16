# A How To Guide - Sentry Integration

## Client Side Error Monitoring and Performance Tracking

**_ Make sure you have access to sentry dashboard and is a member of [second-closet](https://sentry.io/organizations/second-closet/) organization in sentry. _**

### Step 1: Create new sentry project

- Go to [new project](https://sentry.io/organizations/second-closet/projects/new/) in sentry and select React as platform, add a project name and select #second-closet as team.
- Copy dsn for that project. It will look something like this `https://48f8db43cc1544a6a5eec056e8e71244@o207153.ingest.sentry.io/5429850`

### Step 2: Install dependencies

- Run the following command `npm install --save @sentry/react @sentry/tracing`

### Step 3: Copy pasta

- Go to a project with existing sentry implementation and copy `lib/sentry` folder
- Copy `makefile` and paste it on the root of the project
- In your package.json add `&& npm run sentry-release` to the build script
- Add `"sentry-release": "VERSION=$npm_package_version make setup_release",` in your scripts

### Step 4: Change env variables

- Go to your .env file and create a `REACT_APP_SENTRY_DSN` the value should be the one you just copied on step 1.
- Also add `SENTRY_AUTH_TOKEN=697b607c8ef2...` (sentry will use this to create new release and upload source map for the project)

### Step 5: Update makefile script

- Open make file and update the following
- `SENTRY_PROJECT=` (should match sentry project name you just created)
- `REPOSITORY=SecondCloset/` (should match github repo)

### Step 6: Initialize sentry on you app

- Open index.tsx/jsx and import `sentryInit` and `ErrorBoundary` from `lib/sentry`
- Call sentryInit before ReactDOM render and wrap main app component with ErrorBoudary
- If you want to track app performance and pofiling go to your main app component import `withProfiler` hoc from sentry
- If your project uses redux and you want the current store state shown on sentry go to where you initialized your redux store and import `sentryReduxEnhancer`

### Step 7: Track API issues

- At this point if you run your app it will capture client side issues like ReferenceError or TypeError etc. We also want to track the API's when it fails to do this just go to all files you're calling an API and in the `catch` method simply call `reportAPI` from sentry.
- GET/DELETE method `reportAPI(error)`
- POST/PUT method `reportAPI(error, {whatever was the payload sent to the server})`

## Testing locally

- To test if your app is properly hooked up simply call a method that was not defined like `<button onClick={methodDoesNotExist}>Break the world</button>`

## Slack Notifications

- Go to [alerts](https://sentry.io/organizations/second-closet/alerts/) and select the project
- Click `rules` update current rule from sending an email to slack notification
- On alerts contidions add action send slack notif, select second closet and `#sentry-notificaiton` as workspace.

## GitHub Integration

- Go to setting/integration/ [select github](https://sentry.io/settings/second-closet/integrations/github/)
- Click configure then add repository

All set! Dont forget to test your application and try to bundle it locally before deploying to heroku.
