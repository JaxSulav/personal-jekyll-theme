---
layout: post
section-type: post
title: From Mundane to Motivated - How to Add Daily Quotes to Your Gmail Signature
category: Misc
tags: [ 'misc']
---

`This post contains a guide on how to automate the contents of your Gmail signature (Random Daily Quotes in this case)`

# Quotable API:

> There are other options in the market such as API ninjas, zen quotes API and so on but we will use quotable.io here.

The quotable.io provides an API endpoint which we can use to get a random quote each time we send a GET request.

![quotable](/img/posts/auto-quote/quotable-demo.jpg)

> Showing off my cool terminal ASCII art :p. Visit [here](http://www.ascii-art.de/ascii/) for cool ASCII art. 

> Visit [here](https://patorjk.com/software/taag/#p=display&f=Graffiti&t=Type%20Something%20) to convert your texts to ascii art

You can see if we do `curl https://api.quotable.io/random`, we get `JSON` key-value pairs. We can also use `curl https://api.quotable.io/random\?tags=technology,famous-quotes` for quotes that belong to specific types. See the [documentation](quotable.io) from Quotable for more options.


# Step 1: Create Script in Google App Scripts

Going straight into the project, the first step you need to perform is to go this the [Google App Scripts](https://script.google.com/) and log in with your Gmail account.

You should see a window similar to this.

![appscript](/img/posts/auto-quote/app_script.jpg)

> Click on the `New Project` button.

You should see something like this:

![newproject](/img/posts/auto-quote/new_project.jpg)

> Delete function myFunction(){} and add this code to the console:

```javascript
function dailyQuoteUpdate() {
  var response = UrlFetchApp.fetch("https://api.quotable.io/random");
  var quoteData = JSON.parse(response.getContentText());

  var signature = `Best,<br>John Doe<br><br><i><u>Quote of the day</i></u>: <i>"${quoteData.content}" — ${quoteData.author} </i>`;
  
  var resource = {
    signature: signature
  };
  
  console.log(quoteData)
  var userEmail = Session.getActiveUser().getEmail();
  Gmail.Users.Settings.SendAs.patch(resource, userEmail, userEmail);
}
```
<br>

## <u>Components:<u/>

### UrlFetchApp & JSON.parse : 
Send an HTTP GET request to the `quotable.io` API's `/random` endpoint which returns a random quote. The `JSON.parse()` will give us a javascript object `quoteData` to get the values we want using `quoteData.key`. We want `quoteData.content` and `quoteData.author` as seen in the above demo of quotable.io.

### Define and Store Signature : 
Create a `signature` object which will contain the defined signature. We use the values from `quoteData` here as mentioned above.

### Log the data :
We can log the API response data using `console.log(quoteData)`

### Get your email from the current session :
We need to identify whose signature needs to be updated. We can get the current session user's email using `Session.getActiveUser().getEmail();`.

### Update settings for the retrieved user email :
`Gmail.Users.Settings.SendAs.patch` allows us to change just certain parts of the settings: the signature in this case. We have defined resources as:

```js
var resource = {
    signature: signature
  };
```

So, the signature will be updated to the custom signature we just created.


# Step 2: Deploy

> The images speak for themselves: 

![deplopy](/img/posts/auto-quote/deploy.jpg)

![deplopy1](/img/posts/auto-quote/deploy1.jpg)

![deplopy2](/img/posts/auto-quote/deploy2.jpg)

![deplopy3](/img/posts/auto-quote/deploy3.jpg)

> Save your URL

# Step 3: Test Run the Script

> You might face this error while running the script: (Press on `Execution log` if you cannot see the error)

![error](/img/posts/auto-quote/error.jpg)

## Add Gmail API service:

![service](/img/posts/auto-quote/service.jpg)

![service1](/img/posts/auto-quote/service1.jpg)

## You will see Gmail API here:

![service2](/img/posts/auto-quote/service2.jpg)

## Run the code again:

`You will be asked to Review Permission`

![permission0](/img/posts/auto-quote/allow0.jpg)

`You will be asked to Allow Permission for the Script`

![permission](/img/posts/auto-quote/allow.jpg)

## Now, the code should execute successfully :

![success](/img/posts/auto-quote/success.jpg)

### `Your new email signature should be there now.`

# Step 4: Check the Gmail signature

### Go to the settings in your gmail:

![settings](/img/posts/auto-quote/settings.jpg)

### Scroll down until you see the `Signature` section:

![settings1](/img/posts/auto-quote/settings1.jpg)

`Your signature is changed now!!`

# Setp 4: Trigger a random quote daily

### Go to the side menu in the App Script Console and Select `Triggers`

![trigger](/img/posts/auto-quote/trigger.jpg)

### Setup the trigger:

- Select your function from the first dropdown
- Select `Time-driven` for event source
- Select `Day timer` for trigger type
- Select the time you want the trigger to run the script automatically in the time section

<br>

![trigger1](/img/posts/auto-quote/trigger1.jpg)

### You should have this when you compose a new email now: 

![trigger1](/img/posts/auto-quote/final.jpg)

`Congratulations! You now have a daily motivation for yourself and your connections!`

### Resources:
- https://developers.google.com/gmail/api/reference/rest/v1/users.settings.sendAs/create
- https://developers.google.com/apps-script/reference/mail/mail-app
- https://github.com/lukePeavey/quotable
- https://stackoverflow.com/questions/42651005/set-email-signature-using-google-apps-script-with-gmail-api
