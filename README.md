# embed

Blue Jeans offers an easy to use script library for inclusion on your page in order to instantiate the meeting room.  A simple JavaScript object called BJN_CLIENT is setup in advance of the script include to setup the meeting.

## Variables

This table presents a list of various properties that can be set on the BJN_CLIENT object before including embed.js.

<table class="table table-striped table-bordered">
  <tr>
    <th>Name</th><th>Required</th><th>Type</th><th>DescriptionM</th>
 </tr>
 <tr>
 <td>content</td><td>No</td><td>String</td><td>ID of HTML DOM element in which to create the meeting.  If not provided, the content is added inline with a document.writeln.</td>
 </tr>
 <tr>
 <td>meetingId</td><td>Yes</td><td>String</td><td>Blue Jeans meeting ID</td>
 </tr>
 <tr>
 <td>pin</td><td>No</td><td>String</td><td>Moderator pin or attendee pin for the meeting.  If no pin, then do not include property.</td>
 </tr>
 <tr>
 <td>name</td><td>No</td><td>String</td><td>Name of the user joining.  If not provided, user will be prompted.</td>
 </tr>
 <tr>
 <td>email</td><td>No</td><td>String</td><td>Email address of the user joining.</td>
 </tr>
 <tr>
 <td>width</td><td>No</td><td>String</td><td>Used to define the width of the IFRAME for the meeting.  Treated as a string so % can be used. Default is 100%.</td>
 </tr>
 <tr>
 <td>height</td><td>No</td><td>String</td><td>Used to define the height of the IFRAME for the meeting.  Treated as a string so % can be used. Default is 600 pixels.</td>
 </tr>
 <tr>
 <td>onJoin</td><td>No</td><td>Function</td><td>Provide a function that will be called upon launch of the meeting.</td>
  </tr>
</table>

This table presents a list of various properties that are set on BJN_CLIENT for you.  They are normally to be read in cases where you might need to inspect the setup.

<table class="table table-striped table-bordered">
  <tr>
<th>Name</th><th>Type</th><th>Description</th>
</tr>
<tr>
<td>version</td><td>Integer</td><td>A version number for the embed.js script.  This may help in backwards-compatability in the future.</td>
</tr>
<tr>
<td>protocol</td><td>String</td><td>Set to "http:" or "https:" based on where embed.js was loaded from.</td>
</tr>
<tr>
<td>hostname</td><td>String</td><td>The hostname that embed.js was loaded from.</td>
</tr>
</table>

## Script Tag

It is helpful to place an HTML ID on the script include named "bjn-embed".  This is used by the embed.js to detect the hostname used for situations where your implementation is running on different Blue Jeans partitions (production, beta, etc).

## Query Parameters

When launching a Blue Jeans meeting, there are various parameters that can be set to customize the experience.  The embed.js script will setup a variety of these parameters in according to values set on the BJN_CLIENT object.  If you are using the embed.js option, these query parameters are not used directly as embed.js will handle them for you.  However, some implementations may need further customizations so this is provided a reference.

<table class="table table-striped table-bordered">
  <tr><th>Name</th><th>Type</th><th>Description</th></t dr>
<tr><td>embed</td><td>Boolean</td><td>True signals Blue Jeans to use the embedded user interface, which removes branded headers and footers from the page.</td></tr>
<tr><td>fullscreen</td><td>Boolean</td><td>True signals the meeting client to utilize the full width and height that is has been allocated in its parent window/frame.</td></tr>
<tr><td>name</td><td>String</td><td>The name of the user joining the meeting.</td></tr>
<tr><td>email</td><td>String</td><td>The email address of the user joining the meeting.</td></tr>
</table>


## Defer

<p>Depending on your use case, you may not want the &lt;script&gt; tag to automatically start your meeting.  One such situation is when you have a list of meeting and you may want a user to choose one before proceeding.  In this case, you may use a special query parameter to the script called "defer".  This will keep the &lt;script&gt; from starting the meeting.</p>

<pre>&lt;script id="bjn-embed" src="http://bluejeans.com/static/js/embed.js?defer=true"&gt;&lt;/script&gt;</pre>

<p>After using the defer tag, you will need to start the meeting when ready.  To do that, you can call functions that have been added to BJN_CLIENT:</p>

<table class="table table-striped table-bordered">
  <tr>
    <th>Name</th><th>Arguments</th><th>Description</th>
  </tr>
  <tr>
    <td>launch()</td><td>callback function</td><td>Launches the meeting in a new tab with id "bluejeans".  This is an option if you do not want to embed the meeting into your page, but a separate window.</td>
  </tr>
  <tr>
    <td>load()</td><td>callback function</td><td>Launches the meeting inside your prescribed content area configured in BJN_CLIENT.</td>
  </tr>
</table>

## Sample

A sample implementation demonstrating the pieces working together.

<pre>
&lt;html&gt;
        &lt;body&gt;
                &lt;h1>embed.js Demo&lt;/h1&gt;
                &lt;div id="myclient">&lt;/div&gt;
                &lt;script type="text/javascript"&gt;
                        var BJN_CLIENT =
                        {
                                content: 'myclient',
                                meetingId: '8336872800',
                                pin: '4267',
                                name: 'Steve Jobs',
                                email: 'steve@apple.com'
                        };
                &lt;/script&gt;
                &lt;script id="bjn-embed" src="http://bluejeans.com/static/js/embed.js">&lt;/script&gt;
        &lt;/body&gt;
&lt;/html&gt;
</pre>
