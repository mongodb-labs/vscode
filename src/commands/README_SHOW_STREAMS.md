# Show Streams Extension Command

The `Show Streams` command in the MongoDB extension aims to display stream graphs graphically using the flowchart tool `mermaid.js`. The graph should look something like the image below:

<img width="1464" alt="Screen Shot 2023-02-07 at 11 21 51 am" src="https://user-images.githubusercontent.com/100674217/218936000-0eb4d41c-97ca-4218-afaa-109047052a57.png">

# Why mermaid?

After looking at various of the other suggested plugins, mermaid by far had the easiest learning curve and it also had a ‘Markdown Preview’ extension that allowed you to see your graphs in VSCode without needing a WebView
However, it should be noted that mermaid is not as interactive as some other plugins like react-flow.

In order to use `mermaid` you may need to:
`npm install –save mermaid`

This should add `mermaid` into in `packages.json` file.

# Work still needed

Note that this extension command was not fully finished as at the time of implementation, it was not possible to connect the extension command input to the 
output in the shell. Some pseudo code has been written for when the backend for the streams dependencies is fixed:

```
const dataService = this._connectionController.getActiveDataService();
if (dataService === null) {
   alert();
   return false;
}
let nodeParent;
dataService.command('admin', { listStreams: 1, dependencies: true }, (streams) => {})
```

Currently the input is a static variable called `nodeParent`. The format of the input should be as below.
```
// Note: streamA is the root so its parent is an empty string
// The general structure is: 
// {streamName: {'parent': parentNodeName, 'status': status}}
{
'streamA': { 'parent': '', 'status': 'RUNNING' },
'streamB': { 'parent': 'streamA', 'status': 'RUNNING' },
'streamC': { 'parent': 'streamA', 'status': 'STOPPED' },
'streamD': { 'parent': 'streamB', 'status': 'STOPPED' },

 };
```

The code below accepts output from the shell and formats it as necessary for the extension command:
[graphInfo.txt](https://github.com/mongodb-labs/vscode/files/10739601/graphInfo.txt)

