# When to test

You will know if something is ready to test once it has been moved into the `QA` or `verify` column on the project board. 

Once you have tested a story and verified it works you should move it into `code review` or `done`. Which columns are applicable will depends on the project you are working on just take a look at the project board to find out which ones you need.

# How to test

## Lanching the application

Device and browser testing can sometimes be tricky when things are still in development but we now have a continual integration platform that allows us to easily build a version of the code to test.

[Here are the steps](https://github.com/idearium/teamly/blob/master/docs/environment-ote.md) to use the platform.

You will need a [codefresh account](https://g.codefresh.io/). Please let one of the team know if you do not have access.

## Good practice

It is good practice to have the developer tools of a browser open while you are testing to try and capture errors. [Chrome developer tools](https://developer.chrome.com/devtools) are the most user friendly.

## Make it break

When we test, we only ever test what we think should work. Not what people might do when they are clicking around everywhere. Please try your hardest to break things. Do silly things. Try things that you know might break the application. Some examples are;

- Upload a huge file or the wrong file type to an import
- While a page is still loading try clicking all the buttons
- Use the back buttons
- Subscribe and try to subscribe again

# What to test

When testing web applications at Idearium you will need to appropriately [browser and device test](./testing/guide.md) to our standards.

Many Idearium applications have multiple user types. A basic example would be an admin user and a read-only user. For the specific project you are working on you will need to test all user groups and ensure they have the correct access to each feature.

# Documentation

If you find issues when you are testing, detailed documentation is key to giving the developer enough information to quickly resolve the issue. Consider using the most appropriate technique or combination of techniques from below;

- Where you can, include a screen recording of the issue.
- Detail the steps required to recreate the issue.
- Include specific URLS.
- List the relevant user groups.
- List the browser and device the issues was found on.
