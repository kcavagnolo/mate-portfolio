# Personal Portfolio POC

An accessible and fast portfolio built with Gatsby.

[![Travis Status](https://travis-ci.com/kcavagnolo/mate-portfolio.svg?token=Trtw5wviXy4sipUgT6Lm&branch=master)](https://travis-ci.com/kcavagnolo/mate-portfolio)
[![Netlify Status](https://api.netlify.com/api/v1/badges/59e9986a-c9f6-475f-959e-46d00cd5ab6b/deploy-status)](https://app.netlify.com/sites/kcavagnolo/deploys)
[![This project is using Percy.io for visual regression testing.](https://percy.io/static/images/percy-badge.svg)](https://percy.io/Primordial-Analytics/personal-portfolio)

## Setup

1. [Set up Gatsby dev](https://www.gatsbyjs.org/tutorial/part-zero/).
2. Create an empty space at [Contentful](https://www.contentful.com/).
3. Navigate to Settings --> API keys and copy:
   - `Space ID`
   - `Content Delivery API - access token`
   - `Personal Access Token`
4. Run the setup script:

   ```bash
   yarn setup
   ```

5. Launch the dev site locally:

   ```bash
   yarn start
   ```

Access the local dev site at [http://localhost:8000/](http://localhost:8000/).

## Build Site

Environment variables are stored in the `.env` file and is excluded via the `.gitignore` file. To deploy the website, add `SPACE_ID` and `ACCESS_TOKEN` with all `build` commands. The result of builds flow into the `public` folder. On Netlify, do the following:

1. Navigate to Build & deploy --> Environment
2. Click "Edit variables"
3. Add a "New variable"
4. Add and set `ACCESS_TOKEN` to the Contentful `Content Delivery API - access token` from above
5. Add and set `SPACE_ID` to the Contentful `Space ID` from above
6. Navigate to Build & deploy --> Build settings and set "Build command" to:

   ```bash
   SPACE_ID=$SPACE_ID ACCESS_TOKEN=$ACCESS_TOKEN yarn build
   ```

## Adding your information 📝

All the text of this starter live inside Contentful, specifically inside the Content of `About`. In order to change it, just go to `Content` section and change the entity of About with the information you want.

![Contentful About change](./media/contentful-about-change.png)

Regarding the projects and social links the process is the same! Contentful is really easy to learn so don't be afraid of breaking everything, remember that you can restore to the start point by running `yarn setup` 😄

## End to End Testing with Cypress 🧪

The starter comes with a built in End to End Setup using Cypress. As there are no complex logic flow, there are only two tests in place:

1. Accessibility check: using the [cypress-axe](https://www.npmjs.com/package/cypress-axe) plugin you can easily check a lot of a11y rules at once powered by [Axe](https://www.deque.com/axe/)!
2. Visual testing: using [percy-cypress](https://github.com/percy/percy-cypress) plugin you can take screenshot with different resolutions and easily the difference inside their platform. [Here](https://percy.io/Ema-suriano/gatsby-starter-mate) you can check the Percy dashboard for this project.

### Setting Visual Testing for your project (Optional) 📸

By default, the visual testing will fail due to Percy needs a Token in order to know with which project of your account is related. The steps to set up your own visual testing workflow is:

- Create a project in [Percy](https://percy.io/).
- Go to "Project settings" -> "Project token" and copy the whole line saying "PERCY_TOKEN=<YOUR_TOKEN>".
- Open the `.env` file located in the root of the project and add the token to your credentials.
- Try running `yarn e2e:ci` and you should be able to see a new build inside your Project Dashboard in Percy.

## Configuration (Optional) 👷‍♂️

Mate starter is a SPA (Single Page Application), so basically you have only two pages:

- `Main.js`: portfolio itself
- `404.js`: 404 error page with the same style

The structure for the main page is the following:

```javascript
<Layout>
  <Landing />
  <About />
  <Projects />
  <Writing />
</Layout>
```

`Layout` is the core of the application, it manages the theme for the application, the navigation between sections, also it defines the `header`.

All the components inside `Layout` are `Section` components. A section can have a link inside the `Header` or not, in order to add you need to wrapped the exported `Section` with `withNavigation` HOC and it will be automatically registered (Context magic ✨).

## Tracking with Google Analytics (Optional) 📈

This starter has the analytics plugin inside the `gatsby-config`, so the only need to do in order to enable it is to provide the `Tracking Id` for your site (starts with `UA-`). Just set a new variable inside your `.env` file called `ANALYTICS_ID` and analytics will be turn on automatically 😄

## Update your Starter (Optional) 💡

In case you cloned this repository before and you want all the latest changes of it, you can execute the following command to update the code in your repository with the one in this repository:

```bash
# Add repository remote entry
$ git remote add mate https://github.com/EmaSuriano/gatsby-starter-mate

# Get changes from master branch of gatsby-starter-mate
$ git pull mate master --allow-unrelated-histories

# Reset changes in unnecessary folder/files
$ git reset media/ bin/ README.md manifest-config.js

# Remove files affected by the reset
$ git checkout .

# In this step you might need to fix a lot of conflicts, you can do fix manually or use just accept all the changes from mate
$ git checkout --theirs .

# WATCH OUT that some configuration can be overwritten in this last step, like package.json, colors, etc. I highly recommend to do an overall look up at the end of fixing the conflicts.

# Install in case there is any new dependency added to the starter
$ yarn

# Build the project to see if everything is working as expected
$ yarn build
```

## Deployment Automation (Optional) ⚙️

Every time you made a change in your Contentful data or you add a new post in Medium you need to trigger a manual deployment, which can be an annoying task. Therefore I found a nice way to make this process automatic and it is by using a tool called Zapier.

This tool will be watching for changes in Contentful and Medium and then trigger a new deploy in Netlify (or the service you are using). In summary, you don't need to care anymore about deploying your application and can focus on writing content or developing features!

In case you want to know more I wrote an article in Medium that explains the whole process especially for this starter 🙌 [Click here to read it.](https://medium.com/@emasuriano/make-any-static-site-dynamic-without-coding-9dde5673b1a)

**UPDATE:** Contentful added a feature to link it with Netlify as a built in option, but in case you are using another provider I recommend going with Zapier!

## Maintenance

### Lighthouse

[Lighthouse](https://developers.google.com/web/tools/lighthouse) is an open-source, automated tool for improving the quality of web pages. To use:

```bash
npm install -g lighthouse
lighthouse https://kcavagnolo.netlify.com/
```

## Credits

- [Mate Starter Template](https://github.com/EmaSuriano/gatsby-starter-mate) -- EmaSuriano's template
- [Gatsby](https://www.gatsbyjs.org/) -- React and GraphQL website framework
- [Rebass](https://rebassjs.org/) -- styled component system
- [React Reveal](https://www.react-reveal.com/) -- animation framework for React
- [Contentful](https://contentful.com) -- dynamic content
- [font-awesome](https://fontawesome.com/) -- fonts and icons
- [Netlify](https://www.netlify.com) -- build, test, and deploy
- [Medium](https://medium.com) -- blogging
- [Axe](https://www.deque.com/axe/) -- A11y testing
- [Percy](https://percy.io/) -- visual testing

## License

This work is licensed under the [MIT License](LICENSE).
