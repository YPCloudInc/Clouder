# FormBot

In this tutorial, you will be useing Google Apps Script and fBuilder to setup 
"automatically sent message notifications" to a Telegram Group (and/or an Email address) every time a person submits your Google Form

Before things get started, receive the Telegram Chat ID of the group you want to have response messages sent by adding "Get My ID (tg bot)" to a Telegram Group (remove the bot after receiving the Chat ID), and make sure "Pinponboy (tg bot)" is a member of that group

## 1. Create a new Google Form
via https://drive.google.com/ or https://docs.google.com/forms/

<img src="https://i.imgur.com/Ow95By2.png" width=750 height=474>

## 2. Name the Form, add 2~3 Questions

Make sure to have a question where the respondent has to fill in their email. 

## 3. Open Apps Script Editor
<img src="https://i.imgur.com/mLfLP5b.png" width=750 height=474>


## 4. Replace content of code.gs with Webhook Script
* Remember to Rename the project

<img src="https://i.imgur.com/nKLBl29.png" width=750 height=474>

Webhook Script example: 
```
var POST_URL = "https://webhook.ypcloud.com/form";

function onSubmit(e) {
    var form = FormApp.getActiveForm(); 
    var allResponses = form.getResponses();
    var qFormName = form.getTitle();
    var qFormTitle = DriveApp.getFileById(form.getId()).getName();
    var timestamp = new Date().getTime();
    
    var date = new Date(timestamp);
    var formattedTime = (date.getDate()+
          "/"+(date.getMonth()+1)+
          "/"+date.getFullYear()+
          " "+(date.getHours()+1)+
          ":"+date.getMinutes()+
          ":"+date.getSeconds());

    var sReplyNum = FormApp.getActiveForm().getResponses().length;
    var latestResponse = allResponses[allResponses.length - 1];
    var response = latestResponse.getItemResponses();

    var content = {
        "qFormId":"HR-FORM-002",
        "qBot":"exbot",
        "qTgId":"-452345851",
        "qFormName":qFormName,
        "qFormTitle":qFormTitle,
        "qBcc":"",
        "sReplyDate": formattedTime,        
        "sReplyNum": sReplyNum,
        "uName":response[0].getResponse(),
        "uEmail":response[1].getResponse(),
        "uTime":response[2].getResponse(),
        "uResume":response[3].getResponse(),
        "uNote":response[4].getResponse()
        
        
    };
    

    var options = {
        "method": "post",
        "contentType": "application/json",
        "payload": JSON.stringify(content)
    };

UrlFetchApp.fetch(POST_URL, options);
};

```


### Edit var Content （in code.gs)
- qFormId: Replace BW with your initials, modify 01 as necessary
- qbot: Replace with your bot name
- qTgID: Replace with the Chat ID of the Telegram group you want form responses to be sent to
- qBcc: Add any emails you want responses 
- Responses: Change the names and response number based on your form questions

Click "Save" after editing 

### Add a new Trigger
Go to the "Triggers" page

<img src="https://i.imgur.com/HsiFZap.png" width=auto height=auto>

Click "Add Trigger"

<img src="https://i.imgur.com/J2ob7k6.png" width=auto height=auto>

In the dropdown menu for "Select event type", select "On form submit", then click "Save"

<img src="https://i.imgur.com/dH1DWcH.png" width=auto height=auto>

Accept Apps Scripts authorization requests

<img src="https://i.imgur.com/UczqhD5.png" width=auto height=auto>

<img src="https://i.imgur.com/JfRNW8w.png" width=auto height=auto>

<img src="https://i.imgur.com/tLkRP73.png" width=auto height=auto>


Close the Apps Script

## 5. Create your formBot through fBuilder

Login https://run.ypcloud.com, choose "fBuilder", click "Go"

Create a new project

<img src="https://i.imgur.com/BZdmxFZ.png" width=auto height=auto>

Project Name, Title and QName (name of your Bot)

<img src="https://i.imgur.com/fe5mCEB.png">


## 6. Import [formbot-coffee.flow](/coffee/formbot-coffe.flow)
- Edit the funtion node of the `reg` as the comment node shows
- Click "Done", then "Deploy" to save your changes
- Edit the `to email` function nodes: modify `msg.payload` (following `"content"`) according to responses in your Google Form's webhook script

<img src="https://i.imgur.com/MGwpTHl.png">


## 7. Deploy and QRun to q11

## 8. Go to IOCWatch to find your Bot's QRun location

https://iocwatch.ypcloud.com/ 

- Click on ![](https://i.imgur.com/snCgdGt.png) to go the Control panel
- Find and click on `q11/qbix/dc` in the left sidebar
- Click on "Info"

- Find your Bot from the list 
- Copy the mma in the first column
(It should look like: `q11/qbix/qx-yourname-3asdfghj-yourbotname-app`)
- Paste it back to the `reg` function node like the comment node shows
- Deploy and QRun to q11 again 

## 9. Test your Form
After QRun, fill in a Google form and test whether the responses will be sent to your Telegram Group or Email
