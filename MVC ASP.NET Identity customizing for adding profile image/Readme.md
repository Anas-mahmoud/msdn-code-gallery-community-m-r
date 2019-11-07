# MVC ASP.NET Identity customizing for adding profile image
## Requires
- Visual Studio 2015
## License
- MIT
## Technologies
- ASP.NET MVC
- ASP.NET Identity
## Topics
- ASP.NET MVC
- ASP.NET Identity
## Updated
- 08/09/2016
## Description

<h1>Introduction</h1>
<p><img id="153425" src="153425-animation.gif" alt="" width="650" height="446"></p>
<ol>
<li>In our previous article wehave explained about how to customizing <a href="https://code.msdn.microsoft.com/ASPNET-MVC-5-Security-And-44cbdb97">
ASP.NET MVC 5 Security and Creating User Role</a> and <a href="https://code.msdn.microsoft.com/ASPNET-MVC-User-Role-Base-e874e7ea" target="_blank">
User Role base Menu Management (Dynamic menu using MVC and AngularJS)</a> </li></ol>
<p>In this article we will see in detail about using ASP.NET Identity in MVC Application</p>
<p>1)&nbsp;&nbsp;&nbsp;&nbsp; To upload and store User Profile Image to AspNetUsers table in SQL Server.</p>
<p>2)&nbsp;&nbsp;&nbsp;&nbsp; Display the authenticated Logged in users Uploaded profile Image in home page and in Title bar.</p>
<p><img id="153426" src="153426-1.png" alt="" width="559" height="241"></p>
<p><em><br>
</em></p>
<h1><span>Building the Sample</span></h1>
<p><strong><span>Prerequisites</span></strong></p>
<p><strong><span>Visual Studio 2015:</span></strong>&nbsp;<span>You can download it from&nbsp;</span><a href="https://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx" target="_blank"><span>here</span></a><span>.</span></p>
<h1><span style="font-size:20px; font-weight:bold">Description</span></h1>
<h2><strong><span>Step 1: Creating Database</span></strong></h2>
<p><span>First we create a database to store all our ASP.NET&nbsp;</span><span>Identity&nbsp;</span><span>details to be stored in our Local SQL Server. Here we have used SQL Server 2014.Run the below script in your SQL Server to create a Database.</span>&nbsp;</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>SQL</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">mysql</span>
<pre class="hidden">---- =============================================                               
---- Author      : Shanu                             
---- Create date : 2016-05-30                               
---- Description : To Create Database     
---- Latest                               
---- Modifier    : Shanu                                
---- Modify date : 2016-05-30                   
---- =============================================  
----Script to create DB  
  
USE MASTER  
GO  
  
 --1) Check for the Database Exists .If the database is exist then drop and create new DB  
  
IF EXISTS (SELECT [name] FROM sys.databases WHERE [name] = 'UserProfileDB' )  
DROP DATABASE UserProfileDB  
  
GO  
  
CREATE DATABASE UserProfileDB  
GO  
  
USE UserProfileDB  
GO  </pre>
<div class="preview">
<pre class="js">----&nbsp;=============================================&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
----&nbsp;Author&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Shanu&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
----&nbsp;Create&nbsp;date&nbsp;:&nbsp;<span class="js__num">2016</span><span class="js__num">-05</span><span class="js__num">-30</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
----&nbsp;Description&nbsp;:&nbsp;To&nbsp;Create&nbsp;Database&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
----&nbsp;Latest&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
----&nbsp;Modifier&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Shanu&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
----&nbsp;Modify&nbsp;date&nbsp;:&nbsp;<span class="js__num">2016</span><span class="js__num">-05</span><span class="js__num">-30</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
----&nbsp;=============================================&nbsp;&nbsp;&nbsp;
----Script&nbsp;to&nbsp;create&nbsp;DB&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
USE&nbsp;MASTER&nbsp;&nbsp;&nbsp;
GO&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;--<span class="js__num">1</span>)&nbsp;Check&nbsp;<span class="js__statement">for</span>&nbsp;the&nbsp;Database&nbsp;Exists&nbsp;.If&nbsp;the&nbsp;database&nbsp;is&nbsp;exist&nbsp;then&nbsp;drop&nbsp;and&nbsp;create&nbsp;<span class="js__operator">new</span>&nbsp;DB&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
IF&nbsp;EXISTS&nbsp;(SELECT&nbsp;[name]&nbsp;FROM&nbsp;sys.databases&nbsp;WHERE&nbsp;[name]&nbsp;=&nbsp;<span class="js__string">'UserProfileDB'</span>&nbsp;)&nbsp;&nbsp;&nbsp;
DROP&nbsp;DATABASE&nbsp;UserProfileDB&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
GO&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
CREATE&nbsp;DATABASE&nbsp;UserProfileDB&nbsp;&nbsp;&nbsp;
GO&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
USE&nbsp;UserProfileDB&nbsp;&nbsp;&nbsp;
GO&nbsp;&nbsp;</pre>
</div>
</div>
</div>
<h2 class="endscriptcode">&nbsp;<strong>Step 2: Create your Web Application in Visual Studio 2015</strong></h2>
<p>After installing our Visual Studio 2015 click Start, then Programs and select Visual Studio 2015 - Click Visual Studio 2015. Click New, then Project, select Web and then select ASP.NET Web Application. Enter your project name and click OK.&nbsp;Select MVC
 and click OK.&nbsp;</p>
<p>&nbsp;</p>
<p><img id="153427" src="153427-2.png" alt="" width="500" height="327"></p>
<p><strong>Step 3: Web.Config</strong><br>
<br>
In web.config file we can find the&nbsp;DefaultConnection&nbsp;Connection string. By default ASP.NET MVC will use this connection string to create all ASP.NET Identity related tables like AspNetUsers, etc. Here in connection string we will be using our newly
 created DB name.</p>
<p>Here in connection string change your SQL Server Name, UID and PWD to create and store all user details in one database.&nbsp;</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>XML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">xml</span>
<pre class="hidden">&lt;connectionStrings&gt;  
    &lt;add name=&quot;DefaultConnection&quot; connectionString=&quot;data source=YOURSERVERNAME;initial catalog=UserProfileDB;user id=UID;password=PWD;Integrated Security=True&quot; providerName=&quot;System.Data.SqlClient&quot;  /&gt;   
 &lt;/connectionStrings&gt;
</pre>
<div class="preview">
<pre class="js">&lt;connectionStrings&gt;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;add&nbsp;name=<span class="js__string">&quot;DefaultConnection&quot;</span>&nbsp;connectionString=<span class="js__string">&quot;data&nbsp;source=YOURSERVERNAME;initial&nbsp;catalog=UserProfileDB;user&nbsp;id=UID;password=PWD;Integrated&nbsp;Security=True&quot;</span>&nbsp;providerName=<span class="js__string">&quot;System.Data.SqlClient&quot;</span>&nbsp;&nbsp;/&gt;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&lt;/connectionStrings&gt;&nbsp;
</pre>
</div>
</div>
</div>
<p>&nbsp;</p>
<h2><strong>Step 4: IdentityModels.cs</strong></h2>
<p>In IdentityModels.cs we need to add the image property to be used for storing our image to database.Now here in ApplicationUser class we will be adding a new property to store the image here we declare the property type as byte like below</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">public class ApplicationUser : IdentityUser
    {
        // Here we add a byte to Save the user Profile Pictuer
        public byte[] UserPhoto { get; set; }
</pre>
<div class="preview">
<pre class="js">public&nbsp;class&nbsp;ApplicationUser&nbsp;:&nbsp;IdentityUser&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">{</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__sl_comment">//&nbsp;Here&nbsp;we&nbsp;add&nbsp;a&nbsp;byte&nbsp;to&nbsp;Save&nbsp;the&nbsp;user&nbsp;Profile&nbsp;Pictuer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;public&nbsp;byte[]&nbsp;UserPhoto&nbsp;<span class="js__brace">{</span>&nbsp;get;&nbsp;set;&nbsp;<span class="js__brace">}</span>&nbsp;
</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;We can find this class inside the In IdentityModels.cs in Model folder</div>
<p><img id="153428" src="153428-3.png" alt="" width="271" height="85"></p>
<p>&nbsp;</p>
<h2><strong>Step 5: MVC </strong><strong>Model Part</strong></h2>
<p>Next in&nbsp;<strong>AccountViewModel.cs</strong>&nbsp;check for the RegisterViewModel and add the properties like below.</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">[Display(Name = &quot;UserPhoto&quot;)]
        public byte[] UserPhoto { get; set; }
</pre>
<div class="preview">
<pre class="js">[Display(Name&nbsp;=&nbsp;<span class="js__string">&quot;UserPhoto&quot;</span>)]&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;public&nbsp;byte[]&nbsp;UserPhoto&nbsp;<span class="js__brace">{</span>&nbsp;get;&nbsp;set;&nbsp;<span class="js__brace">}</span>&nbsp;
</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;<img id="153429" src="153429-4.png" alt="" width="557" height="346"></div>
<p>&nbsp;</p>
<h2><strong>Step 6: Edit Register view to add our upload image</strong></h2>
<p>In Register.cshtml we add the below code to upload images to AspNetUsers table in our DB.</p>
<p>First we add , enctype = &quot;multipart/form-data&quot; in begin form like below.</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>HTML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">html</span>
<pre class="hidden">@using (Html.BeginForm(&quot;Register&quot;, &quot;Account&quot;, FormMethod.Post, new { @class = &quot;form-horizontal&quot;, role = &quot;form&quot;, enctype = &quot;multipart/form-data&quot; }))
{
</pre>
<div class="preview">
<pre class="js">@using&nbsp;(Html.BeginForm(<span class="js__string">&quot;Register&quot;</span>,&nbsp;<span class="js__string">&quot;Account&quot;</span>,&nbsp;FormMethod.Post,&nbsp;<span class="js__operator">new</span><span class="js__brace">{</span>&nbsp;@class&nbsp;=&nbsp;<span class="js__string">&quot;form-horizontal&quot;</span>,&nbsp;role&nbsp;=&nbsp;<span class="js__string">&quot;form&quot;</span>,&nbsp;enctype&nbsp;=&nbsp;<span class="js__string">&quot;multipart/form-data&quot;</span><span class="js__brace">}</span>))&nbsp;
<span class="js__brace">{</span></pre>
</div>
</div>
</div>
<p>&nbsp;</p>
<p>Next we need to customize our Register page to add the HTMl Image Tag for uploading the image.</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>HTML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">html</span>
<pre class="hidden">&lt;div class=&quot;form-group&quot;&gt;
        @Html.LabelFor(m =&gt; m.UserPhoto, new { @class = &quot;col-md-2 control-label&quot; })
        &lt;div class=&quot;col-md-10&quot;&gt;
           
            &lt;input type=&quot;file&quot; name=&quot;UserPhoto&quot; id=&quot;fileUpload&quot; accept=&quot;.png,.jpg,.jpeg,.gif,.tif&quot; /&gt;
             
        &lt;/div&gt;
    &lt;/div&gt;
</pre>
<div class="preview">
<pre class="js">&lt;div&nbsp;class=<span class="js__string">&quot;form-group&quot;</span>&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Html.LabelFor(m&nbsp;=&gt;&nbsp;m.UserPhoto,&nbsp;<span class="js__operator">new</span>&nbsp;<span class="js__brace">{</span>&nbsp;@class&nbsp;=&nbsp;<span class="js__string">&quot;col-md-2&nbsp;control-label&quot;</span>&nbsp;<span class="js__brace">}</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;class=<span class="js__string">&quot;col-md-10&quot;</span>&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;input&nbsp;type=<span class="js__string">&quot;file&quot;</span>&nbsp;name=<span class="js__string">&quot;UserPhoto&quot;</span>&nbsp;id=<span class="js__string">&quot;fileUpload&quot;</span>&nbsp;accept=<span class="js__string">&quot;.png,.jpg,.jpeg,.gif,.tif&quot;</span>&nbsp;/&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/div&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;/div&gt;&nbsp;
</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;<img id="153430" src="153430-5.png" alt="" width="558" height="356"></div>
<p>&nbsp;</p>
<h2><strong>Step 7: MVC <strong>Controller Part</strong></strong><br>
<img id="153431" src="153431-7.png" alt="" width="563" height="352"></h2>
<p>Next in<strong>&nbsp;</strong><strong>AccountController.cs we will update the code in
</strong>Register <strong>post method to customize and store the uploaded user image</strong> in ASP.NET identity database.</p>
<p>In the Register post method we will save the uploaded image to the byte array and use this byte array result to be saved in our users table.</p>
<h2>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">if (ModelState.IsValid)
            {
                 
                // To convert the user uploaded Photo as Byte Array before save to DB
                byte[] imageData = null;
                if (Request.Files.Count &gt; 0)
                {
                    HttpPostedFileBase poImgFile = Request.Files[&quot;UserPhoto&quot;];

                    using (var binary = new BinaryReader(poImgFile.InputStream))
                    {
                        imageData = binary.ReadBytes(poImgFile.ContentLength);
                    }
                }
var user = new ApplicationUser { UserName = model.Email, Email = model.Email };

                //Here we pass the byte array to user context to store in db
                user.UserPhoto = imageData;
</pre>
<div class="preview">
<pre class="js"><span class="js__statement">if</span>&nbsp;(ModelState.IsValid)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">{</span><span class="js__sl_comment">//&nbsp;To&nbsp;convert&nbsp;the&nbsp;user&nbsp;uploaded&nbsp;Photo&nbsp;as&nbsp;Byte&nbsp;Array&nbsp;before&nbsp;save&nbsp;to&nbsp;DB</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;byte[]&nbsp;imageData&nbsp;=&nbsp;null;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__statement">if</span>&nbsp;(Request.Files.Count&nbsp;&gt;&nbsp;<span class="js__num">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">{</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HttpPostedFileBase&nbsp;poImgFile&nbsp;=&nbsp;Request.Files[<span class="js__string">&quot;UserPhoto&quot;</span>];&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;using&nbsp;(<span class="js__statement">var</span>&nbsp;binary&nbsp;=&nbsp;<span class="js__operator">new</span>&nbsp;BinaryReader(poImgFile.InputStream))&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">{</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;imageData&nbsp;=&nbsp;binary.ReadBytes(poImgFile.ContentLength);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">}</span><span class="js__brace">}</span><span class="js__statement">var</span>&nbsp;user&nbsp;=&nbsp;<span class="js__operator">new</span>&nbsp;ApplicationUser&nbsp;<span class="js__brace">{</span>&nbsp;UserName&nbsp;=&nbsp;model.Email,&nbsp;Email&nbsp;=&nbsp;model.Email&nbsp;<span class="js__brace">}</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__sl_comment">//Here&nbsp;we&nbsp;pass&nbsp;the&nbsp;byte&nbsp;array&nbsp;to&nbsp;user&nbsp;context&nbsp;to&nbsp;store&nbsp;in&nbsp;db</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;user.UserPhoto&nbsp;=&nbsp;imageData;&nbsp;
</pre>
</div>
</div>
</div>
</h2>
<p>Here is the complete code of the Register post method&nbsp;</p>
<h2>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">[HttpPost]
        [AllowAnonymous]
        [ValidateAntiForgeryToken]
        public async Task&lt;ActionResult&gt; Register([Bind(Exclude = &quot;UserPhoto&quot;)]RegisterViewModel model)
        {
            if (ModelState.IsValid)
            {
                 
                // To convert the user uploaded Photo as Byte Array before save to DB
                byte[] imageData = null;
                if (Request.Files.Count &gt; 0)
                {
                    HttpPostedFileBase poImgFile = Request.Files[&quot;UserPhoto&quot;];

                    using (var binary = new BinaryReader(poImgFile.InputStream))
                    {
                        imageData = binary.ReadBytes(poImgFile.ContentLength);
                    }
                }


                var user = new ApplicationUser { UserName = model.Email, Email = model.Email };

                //Here we pass the byte array to user context to store in db
                user.UserPhoto = imageData;

                var result = await UserManager.CreateAsync(user, model.Password);
                if (result.Succeeded)
                {
                    await SignInManager.SignInAsync(user, isPersistent:false, rememberBrowser:false);
                    
                    // For more information on how to enable account confirmation and password reset please visit http://go.microsoft.com/fwlink/?LinkID=320771             

                    return RedirectToAction(&quot;Index&quot;, &quot;Home&quot;);
                }
                AddErrors(result);
            }

            // If we got this far, something failed, redisplay form
            return View(model);
        }
</pre>
<div class="preview">
<pre class="csharp">[HttpPost]&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[AllowAnonymous]&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ValidateAntiForgeryToken]&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;async&nbsp;Task&lt;ActionResult&gt;&nbsp;Register([Bind(Exclude&nbsp;=&nbsp;<span class="cs__string">&quot;UserPhoto&quot;</span>)]RegisterViewModel&nbsp;model)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(ModelState.IsValid)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;To&nbsp;convert&nbsp;the&nbsp;user&nbsp;uploaded&nbsp;Photo&nbsp;as&nbsp;Byte&nbsp;Array&nbsp;before&nbsp;save&nbsp;to&nbsp;DB</span><span class="cs__keyword">byte</span>[]&nbsp;imageData&nbsp;=&nbsp;<span class="cs__keyword">null</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(Request.Files.Count&nbsp;&gt;&nbsp;<span class="cs__number">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HttpPostedFileBase&nbsp;poImgFile&nbsp;=&nbsp;Request.Files[<span class="cs__string">&quot;UserPhoto&quot;</span>];&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">using</span>&nbsp;(var&nbsp;binary&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;BinaryReader(poImgFile.InputStream))&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;imageData&nbsp;=&nbsp;binary.ReadBytes(poImgFile.ContentLength);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;user&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;ApplicationUser&nbsp;{&nbsp;UserName&nbsp;=&nbsp;model.Email,&nbsp;Email&nbsp;=&nbsp;model.Email&nbsp;};&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//Here&nbsp;we&nbsp;pass&nbsp;the&nbsp;byte&nbsp;array&nbsp;to&nbsp;user&nbsp;context&nbsp;to&nbsp;store&nbsp;in&nbsp;db</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;user.UserPhoto&nbsp;=&nbsp;imageData;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;result&nbsp;=&nbsp;await&nbsp;UserManager.CreateAsync(user,&nbsp;model.Password);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(result.Succeeded)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;await&nbsp;SignInManager.SignInAsync(user,&nbsp;isPersistent:<span class="cs__keyword">false</span>,&nbsp;rememberBrowser:<span class="cs__keyword">false</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;For&nbsp;more&nbsp;information&nbsp;on&nbsp;how&nbsp;to&nbsp;enable&nbsp;account&nbsp;confirmation&nbsp;and&nbsp;password&nbsp;reset&nbsp;please&nbsp;visit&nbsp;http://go.microsoft.com/fwlink/?LinkID=320771&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="cs__keyword">return</span>&nbsp;RedirectToAction(<span class="cs__string">&quot;Index&quot;</span>,&nbsp;<span class="cs__string">&quot;Home&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AddErrors(result);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;If&nbsp;we&nbsp;got&nbsp;this&nbsp;far,&nbsp;something&nbsp;failed,&nbsp;redisplay&nbsp;form</span><span class="cs__keyword">return</span>&nbsp;View(model);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
</pre>
</div>
</div>
</div>
</h2>
<p>So now we have successfully completed the Image uploaded part to AspNetUsers Table in our local SQL Server Database.</p>
<p>Next we will see how to display the logged in user Image on home page and in menu bar.&nbsp;</p>
<h2><strong>Step 8: </strong><strong>Display User Image in home page</strong></h2>
<p>For displaying this we create a FileContentResult Method&nbsp; to display the image on user home and in menu bar.&nbsp;</p>
<p>Create FileContentResult method in Home controller as UserPhotos to display the image in home page and in Menu bar.</p>
<h2><img id="153432" src="153432-7.png" alt="" width="583" height="352"></h2>
<p>In home controller we create a method named as UserPhotos and return the image to View page for user profile display.</p>
<p>In this method we check for Authenticated (Logged in) users. If the user is not logged In to our web application then I will display he default image as &ldquo;?&rdquo; like below. Here we display the image in both top menu and in home page.</p>
<p><img id="153433" src="153433-8.png" alt="" width="575" height="204"></p>
<p>If the user is authenticated and successfully logged in to our system then we display the logged in user profile picture in home page like below.</p>
<p><img id="153434" src="153434-9.png" alt="" width="576" height="183"></p>
<p>Here is the complete code for check the Authenticated user and return the valid user&rsquo;s image to our View page .This method we created in our Home controller.</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">public FileContentResult UserPhotos()
        {
            if (User.Identity.IsAuthenticated)
            {
            String    userId = User.Identity.GetUserId();

            if (userId == null)
                {
                    string fileName = HttpContext.Server.MapPath(@&quot;~/Images/noImg.png&quot;);

                    byte[] imageData = null;
                    FileInfo fileInfo = new FileInfo(fileName);
                    long imageFileLength = fileInfo.Length;
                    FileStream fs = new FileStream(fileName, FileMode.Open, FileAccess.Read);
                    BinaryReader br = new BinaryReader(fs);
                    imageData = br.ReadBytes((int)imageFileLength);
                    
                    return File(imageData, &quot;image/png&quot;);

                }
              // to get the user details to load user Image
                var bdUsers = HttpContext.GetOwinContext().Get&lt;ApplicationDbContext&gt;();
            var userImage = bdUsers.Users.Where(x =&gt; x.Id == userId).FirstOrDefault();

            return new FileContentResult(userImage.UserPhoto, &quot;image/jpeg&quot;);
            }
            else
            {
                string fileName = HttpContext.Server.MapPath(@&quot;~/Images/noImg.png&quot;);

                byte[] imageData = null;
                FileInfo fileInfo = new FileInfo(fileName);
                long imageFileLength = fileInfo.Length;
                FileStream fs = new FileStream(fileName, FileMode.Open, FileAccess.Read);
                BinaryReader br = new BinaryReader(fs);
                imageData = br.ReadBytes((int)imageFileLength);                 
                return File(imageData, &quot;image/png&quot;);
               
            }
        }
</pre>
<div class="preview">
<pre class="js">public&nbsp;FileContentResult&nbsp;UserPhotos()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">{</span><span class="js__statement">if</span>&nbsp;(User.Identity.IsAuthenticated)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">{</span><span class="js__object">String</span>&nbsp;&nbsp;&nbsp;&nbsp;userId&nbsp;=&nbsp;User.Identity.GetUserId();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__statement">if</span>&nbsp;(userId&nbsp;==&nbsp;null)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">{</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;string&nbsp;fileName&nbsp;=&nbsp;HttpContext.Server.MapPath(@<span class="js__string">&quot;~/Images/noImg.png&quot;</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;byte[]&nbsp;imageData&nbsp;=&nbsp;null;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileInfo&nbsp;fileInfo&nbsp;=&nbsp;<span class="js__operator">new</span>&nbsp;FileInfo(fileName);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;long&nbsp;imageFileLength&nbsp;=&nbsp;fileInfo.Length;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileStream&nbsp;fs&nbsp;=&nbsp;<span class="js__operator">new</span>&nbsp;FileStream(fileName,&nbsp;FileMode.Open,&nbsp;FileAccess.Read);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BinaryReader&nbsp;br&nbsp;=&nbsp;<span class="js__operator">new</span>&nbsp;BinaryReader(fs);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;imageData&nbsp;=&nbsp;br.ReadBytes((int)imageFileLength);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__statement">return</span>&nbsp;File(imageData,&nbsp;<span class="js__string">&quot;image/png&quot;</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">}</span><span class="js__sl_comment">//&nbsp;to&nbsp;get&nbsp;the&nbsp;user&nbsp;details&nbsp;to&nbsp;load&nbsp;user&nbsp;Image</span><span class="js__statement">var</span>&nbsp;bdUsers&nbsp;=&nbsp;HttpContext.GetOwinContext().Get&lt;ApplicationDbContext&gt;();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__statement">var</span>&nbsp;userImage&nbsp;=&nbsp;bdUsers.Users.Where(x&nbsp;=&gt;&nbsp;x.Id&nbsp;==&nbsp;userId).FirstOrDefault();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__statement">return</span><span class="js__operator">new</span>&nbsp;FileContentResult(userImage.UserPhoto,&nbsp;<span class="js__string">&quot;image/jpeg&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">}</span><span class="js__statement">else</span><span class="js__brace">{</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;string&nbsp;fileName&nbsp;=&nbsp;HttpContext.Server.MapPath(@<span class="js__string">&quot;~/Images/noImg.png&quot;</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;byte[]&nbsp;imageData&nbsp;=&nbsp;null;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileInfo&nbsp;fileInfo&nbsp;=&nbsp;<span class="js__operator">new</span>&nbsp;FileInfo(fileName);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;long&nbsp;imageFileLength&nbsp;=&nbsp;fileInfo.Length;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileStream&nbsp;fs&nbsp;=&nbsp;<span class="js__operator">new</span>&nbsp;FileStream(fileName,&nbsp;FileMode.Open,&nbsp;FileAccess.Read);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BinaryReader&nbsp;br&nbsp;=&nbsp;<span class="js__operator">new</span>&nbsp;BinaryReader(fs);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;imageData&nbsp;=&nbsp;br.ReadBytes((int)imageFileLength);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__statement">return</span>&nbsp;File(imageData,&nbsp;<span class="js__string">&quot;image/png&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="js__brace">}</span><span class="js__brace">}</span></pre>
</div>
</div>
</div>
<p>&nbsp;</p>
<h2><strong>Step 9: MVC </strong><strong>View Part</strong></h2>
<p>&nbsp;<strong>Home view Page:</strong></p>
<p><img id="153435" src="153435-10.png" alt="" width="190" height="101"></p>
<p>In Home Index View we write the below code to display our logged in users profile picture.</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>HTML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">html</span>
<pre class="hidden">&lt;h1&gt;Shanu Profile Image ..
    
     &lt;img src=&quot;@Url.Action(&quot;UserPhotos&quot;, &quot;Home&quot; )&quot;  style=&quot;width:160px;height:160px; background: #FFFFFF;  
    margin: auto;
    -moz-border-radius: 60px;
    border-radius: 100px;
    padding: 6px;
    box-shadow: 0px 0px 20px #888;&quot; /&gt;
    &lt;/h1&gt;
</pre>
<div class="preview">
<pre class="js">&lt;h1&gt;Shanu&nbsp;Profile&nbsp;Image&nbsp;..&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;img&nbsp;src=<span class="js__string">&quot;@Url.Action(&quot;</span>UserPhotos<span class="js__string">&quot;,&nbsp;&quot;</span>Home<span class="js__string">&quot;&nbsp;)&quot;</span>&nbsp;&nbsp;style=&quot;width:160px;height:160px;&nbsp;background:&nbsp;#FFFFFF;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;margin:&nbsp;auto;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;-moz-border-radius:&nbsp;60px;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;border-radius:&nbsp;100px;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;padding:&nbsp;6px;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;box-shadow:&nbsp;0px&nbsp;0px&nbsp;20px&nbsp;#<span class="js__num">888</span>;&quot;&nbsp;/&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;/h1&gt;&nbsp;
</pre>
</div>
</div>
</div>
<p>&nbsp;</p>
<p><strong>_Layout.cshtml</strong></p>
<p>To display our logged in user profile picture to be displayed at the top of our page we write the below code in _Layout.cshtml</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>HTML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">html</span>
<pre class="hidden">&lt;div class=&quot;navbar-collapse collapse&quot;&gt;
                &lt;ul class=&quot;nav navbar-nav&quot;&gt;
                    &lt;li&gt; 
                        &lt;img src=&quot;@Url.Action(&quot;UserPhotos&quot;, &quot;Home&quot; )&quot; height=&quot;48&quot; width=&quot;48&quot; /&gt;
                  
                    &lt;/li&gt;
                    &lt;li&gt;@Html.ActionLink(&quot;Home&quot;, &quot;Index&quot;, &quot;Home&quot;)&lt;/li&gt;
                    &lt;li&gt;@Html.ActionLink(&quot;About&quot;, &quot;About&quot;, &quot;Home&quot;)&lt;/li&gt;
                    &lt;li&gt;@Html.ActionLink(&quot;Contact&quot;, &quot;Contact&quot;, &quot;Home&quot;)&lt;/li&gt;
                &lt;/ul&gt;
                @Html.Partial(&quot;_LoginPartial&quot;)
            &lt;/div&gt;
</pre>
<div class="preview">
<pre class="js">&lt;div&nbsp;class=<span class="js__string">&quot;navbar-collapse&nbsp;collapse&quot;</span>&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;ul&nbsp;class=<span class="js__string">&quot;nav&nbsp;navbar-nav&quot;</span>&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;li&gt;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;img&nbsp;src=<span class="js__string">&quot;@Url.Action(&quot;</span>UserPhotos<span class="js__string">&quot;,&nbsp;&quot;</span>Home<span class="js__string">&quot;&nbsp;)&quot;</span>&nbsp;height=<span class="js__string">&quot;48&quot;</span>&nbsp;width=<span class="js__string">&quot;48&quot;</span>&nbsp;/&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/li&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;li&gt;@Html.ActionLink(<span class="js__string">&quot;Home&quot;</span>,&nbsp;<span class="js__string">&quot;Index&quot;</span>,&nbsp;<span class="js__string">&quot;Home&quot;</span>)&lt;/li&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;li&gt;@Html.ActionLink(<span class="js__string">&quot;About&quot;</span>,&nbsp;<span class="js__string">&quot;About&quot;</span>,&nbsp;<span class="js__string">&quot;Home&quot;</span>)&lt;/li&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;li&gt;@Html.ActionLink(<span class="js__string">&quot;Contact&quot;</span>,&nbsp;<span class="js__string">&quot;Contact&quot;</span>,&nbsp;<span class="js__string">&quot;Home&quot;</span>)&lt;/li&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/ul&gt;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Html.Partial(<span class="js__string">&quot;_LoginPartial&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/div&gt;&nbsp;
</pre>
</div>
</div>
</div>
<p>&nbsp;</p>
<p><strong>Step 10: Run the Application</strong></p>
<p>So now we have completed both upload and display part. Let&rsquo;s start run our application and register new user with Image and check for output.</p>
<h1><span>Source Code Files</span></h1>
<ul>
<li><span>shanuMVCProfileImage.zip</span> </li></ul>
<h1>More Information</h1>
<p><em>Update the Web.Config Connection String with your Local DB Connection.Run the SQL Script to create a Database in our SQL server.</em></p>