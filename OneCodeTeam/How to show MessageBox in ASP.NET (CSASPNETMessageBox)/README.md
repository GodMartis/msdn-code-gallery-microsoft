# How to show MessageBox in ASP.NET (CSASPNETMessageBox)
## Requires
- Visual Studio 2010
## License
- MS-LPL
## Technologies
- ASP.NET
## Topics
- messagebox
## Updated
- 06/10/2012
## Description

<h1>Intelligent TextBox contrl via ASP.NET (CSASPNETMessageBox)</h1>
<h2>Introduction</h2>
<p class="MsoNormal">The sample code demonstrates how to create a MessageBox in asp.net, usually we often use JavaScript functions &quot;alert()&quot; or &quot;confirm()&quot; to show simple messages and make a simple choice with customers, but these dialog
 boxes is very simple, we cannot add any different and complicate controls, images or styles. As we know, good web sites always have their own web styles, such as typeface and colors, and in this situation, JavaScript dialog boxes looks not very well. So this
 sample shows how to make an Asp.net MessageBox.</p>
<p class="MsoNormal">This project defines a customize MessageBox class with some necessary properties. For example, title, text, icons, buttons, events, etc. The MessageBox class looks like a windows form MessageBox but not the same, because these two application's
 working mechanism is different, we need display the MessageBox in current web page, rather than open a new page for displaying messages, so we need a Literal control for receiving HTML code and use web service for getting different results.
</p>
<h2>Running the Sample</h2>
<p class="MsoNormal">Please follow these demonstration steps below.</p>
<p class="MsoNormal">Step 1:&nbsp;Open the CSASPNETMessageBox.sln. Expand the CSASPNETMessageBox web application and press Ctrl &#43; F5 to show the TestMessageBox.aspx.
</p>
<p class="MsoNormal">Step 2: We will see only a button control on the page, please click it and you will see a message box. This message box is showing with default style because of we have not set more properties, you can click OK button to close it.</p>
<p class="MsoNormal"><span style=""><img src="59666-image.png" alt="" width="805" height="200" align="middle">
</span></p>
<p class="MsoNormal">Step 3: <span style="">&nbsp;</span>Then we can browse with another test page to see a more complicate MessageBox. In this page, we can choose the OK button or Cancel button to call web service methods and get the result of method.</p>
<p class="MsoNormal"><span style=""><img src="59667-image.png" alt="" width="805" height="197" align="middle">
</span></p>
<p class="MsoNormal">Step 4: Please click OK or Cancel button to see result, The Ok��s screenshot:<span style="">
</span></p>
<p class="MsoNormal"><span style=""><img src="59668-image.png" alt="" width="545" height="494" align="middle">
</span></p>
<p class="MsoNormal">Step 5: Validation finished.</p>
<h2>Using the Code</h2>
<p class="MsoNormal">Code Logical: </p>
<p class="MsoNormal">Step 1. Create a C# &quot;ASP.NET Empty Web Application&quot; in Visual Studio 2010 or Visual Web Developer 2010. Name it as ��CSASPNETMessageBox&quot;. Add a folder named ��App_Code��, we can put some code files in this folder. In this
 sample, we need create two class library files, ��MessageBox.cs�� and ��MessageBoxCore.cs��. The MessageBox class includes some basic properties, events, enums and method. Developer can use this class in web form code-behind page for creating an Asp.net MessageBox,
 The MessageBoxCore class is used to store core HTML code of MessageBox. </p>
<p class="MsoNormal">Step 2. Now we can begin to write code in MessageBoxCore.cs file, we can create a new web form page and put HTML code in it for preview, and we also need some other html code to make this custom MessageBox control looks better, here is
 the properties of the MessageBoxCore class introduction:</p>
<p class="MsoListParagraphCxSpFirst" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span>MessageBoxButtonHTML: This string variable is used to create buttons.</p>
<p class="MsoListParagraphCxSpMiddle" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span>MessageBoxHTML: This string variable is used to create the frame of MessageBox, it also includes some CSS styles.</p>
<p class="MsoListParagraphCxSpLast" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span>MessageBoxScript: This string variable is used to generate JavaScript code dynamically.</p>
<p class="MsoNormal">Step 3. You can write or copy the code of MessageBox.cs file in your application, the MessageBox class will make a judgment that generates HTML code by all conditions.</p>
<h3>The following code is use to create MessageBox class.</h3>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
public class MessageBox
 {
     public string MessageText
     {
         get;
         set;
     }


     public string MessageTitle
     {
         get;
         set;
     }


     public MessageBoxIcons MessageIcons
     {
         get;
         set;
     }


     public MessageBoxButtons MessageButtons
     {
         get;
         set;
     }


     public MessageBoxStyle MessageStyles
     {
         get;
         set;
     }


     public List&lt;string&gt; SuccessEvent = new List&lt;string&gt;();


     public List&lt;string&gt; FailedEvent = new  List&lt;string&gt;();


     /// &lt;summary&gt;
     /// Define an Asp.net MessageBox instance.
     /// &lt;/summary&gt;
     public MessageBox()
     {
         this.MessageIcons = MessageBoxIcons.System;
         this.MessageButtons = MessageBoxButtons.Ok;
         this.MessageStyles = MessageBoxStyle.StyleA;
     }


     /// &lt;summary&gt;
     /// Define an Asp.net MessageBox instance.
     /// &lt;/summary&gt;
     /// &lt;param name=&quot;text&quot;&gt;Message Box text property.&lt;/param&gt;
     public MessageBox(string text)
     {
         this.MessageText = text;
         this.MessageIcons = MessageBoxIcons.System;
         this.MessageButtons = MessageBoxButtons.Ok;
         this.MessageStyles = MessageBoxStyle.StyleA;
     }


     /// &lt;summary&gt;
     /// Define an Asp.net MessageBox instance.
     /// &lt;/summary&gt;
     /// &lt;param name=&quot;text&quot;&gt;MessageBox text property.&lt;/param&gt;
     /// &lt;param name=&quot;title&quot;&gt;MessageBox title property.&lt;/param&gt;
     public MessageBox(string text, string title)
     {
         this.MessageText = text;
         this.MessageTitle = title;
         this.MessageIcons = MessageBoxIcons.System;
         this.MessageButtons = MessageBoxButtons.Ok;
         this.MessageStyles = MessageBoxStyle.StyleA;
     }


     /// &lt;summary&gt;
     /// Define an Asp.net MessageBox instance.
     /// &lt;/summary&gt;  
     /// &lt;param name=&quot;text&quot;&gt;MessageBox text property.&lt;/param&gt;
     /// &lt;param name=&quot;title&quot;&gt;MessageBox title property.&lt;/param&gt;
     /// &lt;param name=&quot;icons&quot;&gt;MessageBox icon property.&lt;/param&gt;
     /// &lt;param name=&quot;buttons&quot;&gt;MessageBox button style.&lt;/param&gt;
     public MessageBox(string text, string title, MessageBoxIcons icons, MessageBoxButtons buttons, MessageBoxStyle styles)
     {
         this.MessageText = text;
         this.MessageTitle = title;
         this.MessageIcons = icons;
         this.MessageButtons = buttons;
         this.MessageStyles = styles;
     }


     public string Show(object sender)
     {
         string iconUrl = string.Empty;
         string buttonStyle = string.Empty;
         string buttonHTML = string.Empty;
         string scriptHTML = string.Empty;
         string coreHTML = string.Empty;
         StringBuilder builder = new StringBuilder();
         switch (this.MessageIcons)
         {
             case MessageBoxIcons.None:
                 iconUrl = string.Empty;
                 break;
             case MessageBoxIcons.Warnning:
                 iconUrl = &quot;<img src="ages-1.jpg">&quot;;
                 break;
             case MessageBoxIcons.Error:
                 iconUrl = &quot;<img src="ages-2.jpg">&quot;;
                 break;
             case MessageBoxIcons.Question:
                 iconUrl = &quot;<img src="ages-3.jpg">&quot;;
                 break;
             case MessageBoxIcons.System:
                 iconUrl = &quot;<img src="ages-4.jpg">&quot;;
                 break;
         }
         switch (this.MessageStyles)
         {
             case MessageBoxStyle.StyleA:
                 buttonStyle = &quot;button_classA&quot;;
                 break;
             case MessageBoxStyle.StyleB:
                 buttonStyle = &quot;button_classB&quot;;
                 break;
         }
         switch (this.MessageButtons)
         {
             case MessageBoxButtons.Ok:
                 buttonHTML = MessageBoxCore.MessageBoxButtonHtml;
                 buttonHTML = String.Format(buttonHTML, &quot;OK&quot;, buttonStyle, &quot;Yes();&quot;);
                 builder.Append(buttonHTML);
                 break;
             case MessageBoxButtons.OKCancel:
                 string buttonOKHTML = string.Empty;
                 string buttonCancelHTML = string.Empty;
                 buttonOKHTML = MessageBoxCore.MessageBoxButtonHtml;
                 buttonOKHTML = String.Format(buttonOKHTML, &quot;OK&quot;, buttonStyle, &quot;Yes();&quot;);
                 builder.Append(buttonOKHTML);
                 builder.Append(&quot;&nbsp;&nbsp;&nbsp;&quot;);
                 buttonCancelHTML = MessageBoxCore.MessageBoxButtonHtml;
                 buttonCancelHTML = String.Format(buttonCancelHTML, &quot;Cancel&quot;, buttonStyle, &quot;No();&quot;);
                 builder.Append(buttonCancelHTML);
                 break;
             case MessageBoxButtons.YesOrNo:
                 string buttonYesHTML = string.Empty;
                 string buttonNoHTML = string.Empty;
                 buttonYesHTML = MessageBoxCore.MessageBoxButtonHtml;
                 buttonYesHTML = String.Format(buttonYesHTML, &quot;Yes&quot;, buttonStyle, &quot;Yes();&quot;);
                 builder.Append(buttonYesHTML);
                 builder.Append(&quot;&nbsp;&nbsp;&nbsp;&quot;);
                 buttonNoHTML = MessageBoxCore.MessageBoxButtonHtml;
                 buttonNoHTML = String.Format(buttonNoHTML, &quot;No&quot;, buttonStyle, &quot;No();&quot;);
                 builder.Append(buttonNoHTML);
                 break;
             case MessageBoxButtons.YesNoCancel:
                 string buttonYesCHTML = string.Empty;
                 string buttonNoCHTML = string.Empty;
                 string buttonCancelCHTML = string.Empty;
                 buttonYesCHTML = MessageBoxCore.MessageBoxButtonHtml;
                 buttonYesCHTML = String.Format(buttonYesCHTML, &quot;Yes&quot;, buttonStyle, &quot;Yes();&quot;);
                 builder.Append(buttonYesCHTML);
                 builder.Append(&quot;&nbsp;&nbsp;&nbsp;&quot;);
                 buttonNoCHTML = MessageBoxCore.MessageBoxButtonHtml;
                 buttonNoCHTML = String.Format(buttonNoCHTML, &quot;No&quot;, buttonStyle, &quot;No();&quot;);
                 builder.Append(buttonNoCHTML);
                 builder.Append(&quot;&nbsp;&nbsp;&nbsp;&quot;);
                 buttonCancelCHTML = MessageBoxCore.MessageBoxButtonHtml;
                 buttonCancelCHTML = String.Format(buttonCancelCHTML, &quot;Cancel&quot;, buttonStyle, &quot;No();&quot;);
                 builder.Append(buttonCancelCHTML);
                 break;
         }
         string successName = string.Empty;
         string failedName = &quot;1&quot;;
         StringBuilder successBuilder = new StringBuilder();
         StringBuilder failedBuilder = new StringBuilder();
         if (SuccessEvent != null && SuccessEvent.Count != 0)
         {
             int eventCounts = SuccessEvent.Count;
             for (int i = 0; i &lt; eventCounts; i&#43;&#43;)
             {
                 successBuilder.Append(&quot;PageMethods.&quot;);
                 successBuilder.Append(SuccessEvent[i].ToString());
                 successBuilder.Append(&quot;(null,null,Success, Failed);&quot;);
             }
             successName = successBuilder.ToString();
         }
         if (FailedEvent != null && FailedEvent.Count != 0)
         {
             int eventCounts = FailedEvent.Count;
             for (int i = 0; i &lt; eventCounts; i&#43;&#43;)
             {
                 failedBuilder.Append(&quot;PageMethods.&quot;);
                 failedBuilder.Append(FailedEvent[i].ToString());
                 failedBuilder.Append(&quot;(null,null,Success, Failed);&quot;);
             }
             failedName = failedBuilder.ToString();
         }
         scriptHTML = MessageBoxCore.MessageBoxScript;
         scriptHTML = String.Format(scriptHTML, successName, failedName);
         coreHTML = MessageBoxCore.MessageBoxHTML;
         coreHTML = String.Format(coreHTML, this.MessageTitle, iconUrl, this.MessageText, builder.ToString());
         (sender as Page).ClientScript.RegisterClientScriptBlock(sender.GetType(), &quot;_arg&quot;, scriptHTML, true);
         return coreHTML;
     }


     public enum MessageBoxButtons
     {
         Ok,
         OKCancel,
         YesOrNo,
         YesNoCancel
     };


     public enum MessageBoxIcons
     {
         None,
         Warnning,
         Question,
         System,
         Error
     }


     public enum MessageBoxStyle
     {
         StyleA,
         StyleB
     }
 }

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"></p>
<p class="MsoNormal">Step 4. In MessageBoxCore class, we find that we use some unspecified CSS styles, we need add a CSS file that includes these styles. You can find this information in MessageBox.css file. The another important thing, we can put this CSS
 file and some necessary controls such as ScriptManager and Literal control in a UserControl, because we may use MessageBox control in every page of our project, so I think we must make it easy for re-use, we need only drag and drop this UserControl in our
 web pages and write less code for running.</p>
<p class="MsoNormal">Step 5. After all step finished, we can create some test pages to see our achievement. We can use this MessageBox to show some tips or make a simple choice, in this sample, we can even access web services method by MessageBox class. Here
 is using introduction, remember we need drag and drop that Usercontrol in these pages:</p>
<h3>The following code is use to show some simple messages via MessageBox, very simple.
</h3>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected void btnInvokeMessageBox_Click(object sender, EventArgs e)
{
    MessageBox messageBox = new MessageBox();
    messageBox.MessageTitle = &quot;Information&quot;;
    messageBox.MessageText = &quot;Hello everyone, I am an Asp.net MessageBox. Please put your message here and click the following button to close me.&quot;;
    Literal1.Text = messageBox.Show(this);
}

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<h3><span style="font-family:&quot;Calibri&quot;,&quot;sans-serif&quot;; font-weight:normal"></span></h3>
<h3>The following code shows how to create a little complicate MessageBox that it can make a choice and access web methods.</h3>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected void btnInvokeConfirm_Click(object sender, EventArgs e)
{
    string title = &quot;Confirm&quot;;
    string text = @&quot;Hello everyone, I am an Asp.net MessageBox. You can set MessageBox.SuccessEvent and MessageBox.FailedEvent and Click Yes(OK) or No(Cancel) buttons for calling them. The Methods must be a WebMethod because client-side application will call web services.&quot;;
    MessageBox messageBox = new MessageBox(text, title, MessageBox.MessageBoxIcons.Question, MessageBox.MessageBoxButtons.OKCancel, MessageBox.MessageBoxStyle.StyleB);
    messageBox.SuccessEvent.Add(&quot;OkClick&quot;);
    messageBox.SuccessEvent.Add(&quot;OkClick&quot;);
    messageBox.FailedEvent.Add(&quot;CancalClick&quot;);
    Literal1.Text = messageBox.Show(this);
}


[WebMethod]
public static string OkClick(object sender, EventArgs e)
{
    return &quot;You have clicked Ok button&quot;;
}


[WebMethod]
public static string CancalClick(object sender, EventArgs e)
{
    return &quot;You have clicked Cancel button.&quot;;
}

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"></p>
<p class="MsoNormal">Step 6. Build the application and you can debug it.</p>
<p class="MsoNormal"></p>
<h2>More Information</h2>
<p class="MsoListParagraphCxSpFirst" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><a href="http://msdn.microsoft.com/en-us/library/byxd99hx(v=VS.71).aspx">Using the
<span class="SpellE">WebMethod</span> Attribute</a></p>
<p class="MsoListParagraphCxSpLast" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><a href="http://msdn.microsoft.com/en-us/library/system.enum.aspx"><span class="SpellE">Enum</span> Class</a></p>
<p class="MsoNormal"></p>
<hr>
<div><a href="http://go.microsoft.com/?linkid=9759640" style="margin-top:3px"><img alt="" src="http://bit.ly/onecodelogo">
</a></div>
