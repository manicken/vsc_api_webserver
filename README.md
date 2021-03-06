# api-webserver README

This extension make it possible to take control of Visual Studio Code from a Web Page based client.


## Features

* POST request with data contents in json format:
```
{
    "files":[
        {
            "name":"Main.c",
            "contents":""
        },
        {
            "name":"Main.h",
            "contents":""
        }
    ],
    "removeOtherFiles":true
}
```
in above json:
removeOtherFiles mean that when this is set to true
 then files that is not present in the JSON is removed 
 from the VSCODE project FilesDirectory (described in [Extension Settings](#extension-settings))
 it should be set to false if only known files need to be replaced/added.

* GET request
possible query strings:
```
http://localhost:8080?cmd=getFile&fileName=fileNameWithExt
http://localhost:8080?cmd=compile
http://localhost:8080?cmd=upload
http://localhost:8080?cmd=ping
```
note. that i have prevented directory traversal by the filename
so if you want to use the root src folder to store files in
set the setting to "FilesDirectory": "",

## Requirements
none
## Extension Settings
in webServerApiSettings.json in project root
Contents example:
```
{
    "webServerPort": 8080,
    "webSocketPort": 3000,
    "FilesDirectory": "DesignTool",
    "useTerminalOutputAnsiStrip": true,
    "useTerminalOutputToHtml": true
}
webServerPort: the port that the webserver listen to

webSocketPort: the port that the websocketserver listen to

FilesDirectory: this is the folder where the files will be put by the POST command
                it's also the root folder of getFile

useTerminalOutputAnsiStrip: when this is set the Ansi Style characters is stripped from the terminal capture data

useTerminalOutputToHtml: converts < to &lt;
                                  > to &gt;
                                  \r\n \r \n  respective to <br>
                                  "space char" to &nbsp;

if both useTerminalOutputToHtml and useTerminalOutputAnsiStrip is set
 then the html output will be stripped from the Ansi Style characters
```		         

to apply the settings use the command:
```
API-webserver restart
```
## Known Issues
to use the terminal capture
you need to start VSCODE with the following parameter:
--enable-proposed-api JannikSvensson.api-webserver

in windows just right click on the vs-code shortcut select properties and put it after .exe" line
in windows 10 if you have the shortcut on the start-menu first right click that select "more-open file location"
then right click that and do the above.

in both linux and mac the VSCODE needs to be started from the terminal<br>
(if you don't go througt the complicated thing of creating a shell script)<br>
with:<br>
code --enable-proposed-api JannikSvensson.api-webserver<br>

## Release Notes

### 1.0.0

Initial release of API_Webserver

### 1.0.1

Add GET requests

### 1.0.2

Add Settings file

### 1.0.3

Add terminal capture and send to connected WebSocket client
to use terminal capture use --enable-proposed-api JannikSvensson.api-webserver as VSCODE start parameter

### 1.0.4

Add settings useTerminalOutputCapture, useTerminalOutputToHtml, useTerminalOutputAnsiStrip
Add POST JSON data removeOtherFiles
Fix File write flag so that it overwrites existing files

-----------------------------------------------------------------------------------------------------------
<!---
### For more information

* [Visual Studio Code's Markdown Support](http://code.visualstudio.com/docs/languages/markdown)
 * [Markdown Syntax Reference](https://help.github.com/articles/markdown-basics/)

**Enjoy!**
 -->