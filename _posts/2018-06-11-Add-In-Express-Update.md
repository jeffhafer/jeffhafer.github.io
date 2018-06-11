---
layout: post
title: Add-In Express Cheatsheet
published: true
---
# Add-In Express Cheatsheet

## Example: Calling .Net from Javascript

When setting up an add-in that allows javascript calls to communicate with .Net application, it is important to note that the .Net event for handling the comm should be Initialize(), not IEModule_DocumentComplete. The IEModule_DocumentComplete works to some extent, but an F5 refresh of the browser causes it to fail. Initialize works always. Here is an example showing the necessary .Net code and HTML routines. The .Net code contains a class, MyWinApiWindow, that may or may not be necessary for the application you are running. It allows you to pop-up a messagebox ALWAYS in front of the browser. Sometimes VERY important, sometimes not at all.

```VB.Net
	Public Sub Initialize() Handles MyBase.DownloadComplete
		Try
		Dim scriptEngine As Object = Me.HTMLDocument.Script
		scriptEngine.GetType().InvokeMember("myAddon", BindingFlags.SetProperty, Nothing, scriptEngine, New Object() {Me})
		Catch ex As Exception
		End Try
	End Sub

	Public Sub MyMethod(ByVal param1 As String, ByVal param2 As String)
		  MessageBox.Show(New MyWinApiWindow(Me.ParentHandle), param1 & " " & param2)
	End Sub

	Public Class MyWinApiWindow
		  Implements System.Windows.Forms.IWin32Window
		  Dim theHandle As IntPtr
		  Public Sub New(ByVal aHandle As System.IntPtr)
		  theHandle = aHandle
		  End Sub
		  Public ReadOnly Property Handle() As System.IntPtr _
		  Implements System.Windows.Forms.IWin32Window.Handle
		  Get
			  Return theHandle
		  End Get
		  End Property
	End Class
```


```HTML
<html>
    <head>
  <script type="text/javascript"> 
	var myAddon = null; 
	function MyFunction(){ 
		if(myAddon != null){ 
			myAddon.MyMethod("okay", "dokey"); 
		} else {
			alert("The add-on isn't registered"); 
		}
	}
</script>
    </head>
    <body class='body1'>
  <button id='btn_launch' name='btn_launch' type='button' onClick='MyFunction();'>Launch Button</button>
    </body>
</html>
```

Important

You can see that it is very simple to callback .Net with multiple parameters.

Gettting started:

1. Create a new project

File - New Project - Extensibility - ADX IE Add-on Enter project name. Click OK Click Visual Basic and leave Version-Neutrl mode clicked. Click Next. Leave Generate new selected. Hit Finish.

* This creates the necessary framework code.

2. Add some controls

Right-Click IEModule.vb and choose View Designer. Click on commands and choose Add Click on caption and enter text for command button. Choose an Active and Inactive icon if necessary Choose if you want it show in Menus Add come code to a click event like messagebox.show(“Hello, World”). Hit Close Right-Click the Project name from the Solution Explorer Choose Register ADX Project Should see “The ADX project registration succeeded”. Hit Close.

3. Test by opening IE

You will see a smiley-face in the

4. Add a ContextMenu item Debug in IE

Close IE. Return to project. Right-Click IEModule.vb and choose View Designer Click on ContextMenu (Items). Click on Upper-Right small Icon. This brings up a list of all objects Click on object and then on “Caption” property. Enter some text. Choose Context and Hit OK. Go to properties pane and choose dropdown to see objects Choose your ContextMenu Item Choose Click Event. Enter some code as above. Go to “Project” from top menu. Then choose properties [of project] Choose “Debug” tab. Choose “Start external program:”. Enter “c:\Program Files\Internet Explorer\iexplore.exe” Enter “www.add-in-express.com” in “command line arguments:” This means to run the application/solution/add-in through internet explorer on page: www.add-in-express.com

5. Add a Toolbar (Top of Screen)

Close IE. Return to project. Right-click on project and choose Add - New Item. Choose Add-in Express Items - Internet Explorer - ADX IE ToolBar Right-Click MyIEToolbar1.vb and choose View Designer Add a button to the toolbar Edit button properties Change text Add a click event Right-Click IEModule.vb and choose View Designer Choose “IEModule AddInExpress.IE.ADXIEModule” in Properties dropdown Click Toolbars and you should see your toolbar in the list LoadAtStartup -&gt; True. MenuText -&gt; “My Toolbar” Position -&gt; NewRow Title -&gt; “My Toolbar” ToolBarType -&gt; Choose only one in list Test by running add-on in IE.

6. Add a SideBar ()

Close IE. Return to project. Right-click on project and choose Add - New Item. Choose Add-in Express Items - Internet Explorer - ADX IE Bar Right-Click MyIEBar1.vb and choose View Designer Blah, blah, blah - No reason to get too detaild here. This is much like above

7. Add some events to the add-in

Close IE if open Right-Click on IEModule.vb and choose Properties Choose “IEModule AddInExpress.IE.ADXIEModule” in Properties dropdown Click on the events lightning bolt. Double-click on BeforeNavigate2 to create event Add some code: ”

Tabs

A new IE tab is created when you navigate to a web page or a blank page.

Internet ExplorerProgramming

