<a href="/1.3/README.md">Back to the Table of Contents</a>&nbsp;&nbsp;|&nbsp;&nbsp;<a href="API_METHODS.md">Back to API Methods</a>
<h2>sendSMS</h2>
<p><strong>Synopsis: </strong><br />
This API Sends an SMS from the specified account and short code to a recipient’s mobile number</p>
<div><strong>Request:</strong></div>
<pre>&lt;REQUEST&gt;
  &lt;ACTION&gt;sendSMS &lt;/ACTION&gt;
	&lt;API_KEY&gt;API KEY&lt;/API_KEY&gt;
	&lt;SPID&gt;SPID&lt;/SPID&gt;
	&lt;TO&gt;Recipient Number&lt;/TO&gt;
	&lt;FROM&gt;shortcode&lt;/FROM&gt;
	&lt;CAMPAIGNREF&gt;CampaignID&lt;/CAMPAIGNREF&gt;
	&lt;TEXT&gt;SMS Text message text&lt;/TEXT&gt;
&lt;/REQUEST&gt;</pre>
<div><strong>Request Parameters:</strong></div>

<pre><strong>Mandatory:</strong> Action, API_KEY, To, Text, From
	
<strong>Optional:</strong>SPID, CampaignRef</pre>
	
<p><strong>Response Parameters:</strong><br />

<pre>Status, TrackingID, To, Errorcode, Errorinfo</pre>
	
<strong>Related Error codes: </strong><br />

<pre>E712, E201, E713, E110, E628, E111</pre>
	
<div><strong>Request Example:</strong></div>
<pre>&lt;REQUEST&gt;
    &lt;ACTION&gt;sendSMS&lt;/ACTION&gt;
    &lt;API_KEY&gt;qTFkykO9JTfahCOqJ0V2Wf5Cg1t8iWlZ&lt;/API_KEY&gt;
    &lt;TO&gt;15551234888 &lt;/TO&gt;
    &lt;FROM&gt;60856&lt;/FROM&gt;
    &lt;CAMPAIGNREF&gt;77676&lt;/CAMPAIGNREF&gt;
    &lt;TEXT&gt;Hello Jerry – Greetings from Marc!!&lt;/TEXT&gt;
&lt;/REQUEST&gt;</pre>
<div><strong>Response Example: Success</strong></div>
<pre>&lt;RESPONSE&gt;
	&lt;STATUS&gt;Success&lt;/STATUS&gt;
	&lt;TRACKINGID&gt;SMS_12345&lt;/TRACKINGID&gt;
	&lt;TO&gt;15551234888&lt;/TO&gt;
 &lt;/RESPONSE&gt;</pre>
<div><strong>Response Example: Failure</strong></div>
<pre>&lt;RESPONSE&gt;
	&lt;STATUS&gt;Failure&lt;/STATUS&gt;
	&lt;ERRORCODE&gt;E713&lt;/ERRORCODE&gt;
	&lt;ERRORINFO&gt;There is billing problem on your account&lt;/ERRORINFO&gt;
	&lt;TO&gt;15551234888&lt;/TO&gt;
&lt;/RESPONSE&gt;</pre>
<div><strong>Postback Notification:</strong><br />
When the SMS is sent we will generate a Postback notification.</div>
<pre>&lt;NOTIFICATION  ID="325" CREATED="2011-07-26 10:22:26.975911-04" &gt;
	&lt;ORIGIN&gt;SMS_MT&lt;/ORIGIN&gt;
	&lt;CODE&gt;N201&lt;/CODE&gt;
	&lt;BODY&gt;
	&lt;HISTORYID&gt;236990&lt;/HISTORYID&gt;
	&lt;TO&gt;15551234888&lt;/TO&gt;
	&lt;TRACKINGID&gt;SMS_12345&lt;/TRACKINGID&gt;
	&lt;TIMESTAMP&gt;2011-07-26 10:22:25.262743-04&lt;/TIMESTAMP&gt;
	&lt;/BODY&gt;
&lt;/NOTIFICATION&gt;</pre>
<p>When we get an SMS delivery receipt we will generate another Postback notification. Not all carriers provide SMS delivery receipts.</p>
<pre>&lt;NOTIFICATION id="326" created=" 2011-07-26 10:22:27.146582-04"&gt;
	&lt;ORIGIN&gt;SMS_MT&lt;/ORIGIN&gt;
 	&lt;CODE&gt;N201&lt;/CODE&gt;
	&lt;BODY&gt;
	&lt;HISTORYID&gt;236990&lt;/HISTORYID&gt;
 	&lt;TO&gt;15551234888&lt;/TO&gt;
	&lt;TRACKINGID&gt;SMS_12345&lt;/TRACKINGID&gt;
	&lt;STATUS PROTOCOL="4" STATUS="0"/&gt;
	&lt;TIMESTAMP&gt;2011-07-26 10:22:25.262743-04&lt;/TIMESTAMP&gt;
	&lt;/BODY&gt;
&lt;/NOTIFICATION&gt;</pre>
