<a href="/1.3/README.md">Back to the Table of Contents</a>&nbsp;&nbsp;|&nbsp;&nbsp;<a href="API_METHODS.md">Back to API Methods</a>
<h2>sendSavedMMS</h2>
<p><strong>Synopsis:</strong><br />
This API sends stored content from a specified account using a MMSID to a one or a list of mobile numbers. Recipient addresses are specified by a comma delimited list of valid mobile numbers. List up to 100 numbers is supported. FROM must be one of shortcodes allowed for your account. In case there are numbers from different countries than FROM shortcode is assigned to &#8211; default shortcode for those countries will be used.</p>
<p><strong>Content Transcoding:</strong><br />
Every binary MMS we deliver can be transcoded for the destination handset and every web page we deliver is transcoded for the browsing handset. To transcode a binary MMS we must know what type of handset the user has. We are able to obtain this handset type information from delivery receipts and store the record in a handset cache for later use. We have a database of attributes which we manually match to every new handset in the cache so we can adapt the content during MMS delivery.</p>
<p>Our API allows you to dynamically change each slide text by setting up CUSTOMTEXT (value, slide) and MMS Subject by setting CUSTOMSUBJECT.
<p>A Device Discovery Message (DDM) is a short textual MMS message that is sent to the number to discover what handset the end user is using. We store this handset information in our system and reuse it, so a DDM is sent only to new numbers. If the DDM settings are not included within your API call and the number is not in the handset cache we will deliver the MMS with generic settings. If the handset is in the handset cache the DDM will not be sent and the MMS message will be transcoded and delivered immediately.</p>
<p>Our API allows you to customize DDM by setting 3 parameters:<br />
DDMTITLE &#8211; this is the DDM title<br />
DDMTEXT &#8211; this is the DDM body<br />
DDMTIMEOUT &#8211; when we send DDM we wait for the Delivery Report which contain the handset profile. In some cases we don&#8217;t receive it or it takes very long (handset turned off or out of range). This variable tells the system how long should it wait for DDM Delivery Report before sending actual content using Default parameters. Default value of this parameter is 5 minutes.</p>
<div><strong>Request:</strong></div>
<pre>&lt;REQUEST&gt;
	&lt;ACTION&gt;sendSavedMMS&lt;/ACTION&gt;
	&lt;API_KEY&gt;API KEY&lt;/API_KEY&gt;
	&lt;MMSID&gt;MMSID&lt;/MMSID&gt;
	&lt;TO&gt;Number&lt;/TO&gt;
	&lt;FROM&gt;Shortcode&lt;/FROM&gt;
	&lt;CAMPAIGNREF&gt;CampaignID&lt;/CAMPAIGNREF&gt;
        &lt;DDMTITLE&gt;DDM Title&lt;/DDMTITLE&gt;
        &lt;DDMTEXT&gt;DDM Body&lt;/DDMTEXT&gt;
        &lt;DDMTIMEOUT&gt;DDM Timeout in minutes&lt;/DDMTIMEOUT&gt;
        &lt;CUSTOMTEXT&gt;
        	&lt;VALUE&gt;Custom Text for slide&lt;/VALUE&gt;
        	&lt;SLIDE&gt;Slide ID&lt;/SLIDE&gt;
        &lt;/CUSTOMTEXT&gt;
        &lt;/CUSTOMSUBJECT&gt;MMS Custom Subject&lt;/CUSTOMSUBJECT&gt;
&lt;/REQUEST&gt;</pre>
<div><strong>Request Parameters:</strong></div>
<pre><strong>Mandatory:</strong> Action, API_KEY, MMSID, To, From
<strong>Optional: </strong>CampaignRef, CustomSubject, CustomText</pre>
<strong>Response Parameters:</strong><br />
MMSID, Status, To, TrackingID, Errorcode, Errorinfo

<strong>Related Errorcodes: </strong><br />
E110, E111, E241, E620, E621, E623, E626, E628, E629, E713, E714, E715

<div><strong>Request Example:</strong></div>
<pre>&lt;REQUEST&gt;
	&lt;ACTION&gt; sendSavedMMS &lt;/ACTION&gt;
	&lt;API_KEY&gt;qTFkykO9JTfahCOqJ0V2Wf5Cg1t8iWlZ&lt;/API_KEY&gt;
	&lt;TO&gt;16501234123,16501234124&lt;/TO&gt;
	&lt;FROM&gt;60856&lt;/FROM&gt;
	&lt;CAMPAIGNREF&gt;12333&lt;/CAMPAIGNREF&gt;
	&lt;MMSID&gt;35674&lt;/MMSID&gt;
        &lt;DDMTITLE&gt;We are detecting your handset&lt;/DDMTITLE&gt;
        &lt;DDMTEXT&gt;This message is free of charge and will allow us to deliver your content nice and smooth&lt;/DDMTEXT&gt;
        &lt;DDMTIMEOUT&gt;10&lt;/DDMTIMEOUT&gt;
        &lt;CUSTOMTEXT&gt;
        	&lt;VALUE&gt;My Custom text in first slide&lt;/VALUE&gt;
        	&lt;SLIDE&gt;1&lt;/SLIDE&gt;
        &lt;/CUSTOMTEXT&gt;
        &lt;/CUSTOMSUBJECT&gt;My Custom Subject&lt;/CUSTOMSUBJECT&gt;
&lt;/REQUEST&gt;</pre>
<div><strong>Response Example: Success</strong></div>
<pre>&lt;RESPONSE&gt;
    &lt;STATUS&gt;Success&lt;/STATUS&gt;
    &lt;MMSID&gt;35674&lt;/MMSID&gt;
    &lt;SENDING&gt;
        &lt;TRACKINGID&gt;MMS_12346&lt;/TRACKINGID&gt;
        &lt;TO&gt;16501234123&lt;/TO&gt;
    &lt;/SENDING&gt;
    &lt;SENDING&gt;
        &lt;ERRORCODE&gt;E715&lt;/ERRORCODE&gt;
        &lt;TO&gt;16501234124&lt;/TO&gt;
        &lt;ERRORINFO&gt;Number is not subscribed in this campaign&lt;/ERRORINFO&gt;
    &lt;/SENDING&gt;
&lt;/RESPONSE&gt;</pre>
<div><strong>Response Example: Failure</strong></div>
<pre>&lt;RESPONSE&gt;
	 &lt;STATUS&gt;Failure&lt;/STATUS&gt;
	 &lt;ERRORCODE&gt;E713&lt;/ERRORCODE&gt;
	 &lt;TO&gt;16501234123,16501234124&lt;/TO&gt;
	 &lt;ERRORINFO&gt;There is billing problem on your account&lt;/ERRORINFO&gt;
&lt;/RESPONSE&gt;</pre>
<div><strong>Postback Notifications For SendSavedMMS</strong></div>
<p>When the MMS delivery is processed successfully the system will generate a Postback notification.</p>
<pre>&lt;NOTIFICATION   ID="325" CREATED="2011-08-02 07:20:45.870623-04"&gt;
	&lt;ORIGIN&gt;MMS_MT&lt;/ORIGIN&gt;
	&lt;CODE&gt;N101&lt;/CODE&gt;
	&lt;BODY&gt;
        &lt;HISTORYID&gt;249687&lt;/HISTORYID&gt;
        &lt;MMSID&gt;35674&lt;/MMSID&gt;
        &lt;TO&gt;16501234123&lt;/TO&gt;
        &lt;TRACKINGID&gt;MMS_12346&lt;/TRACKINGID&gt;
        &lt;SPID&gt;000189&lt;/SPID&gt;
        &lt;TIMESTAMP&gt;2011-08-02 07:20:44-04&lt;/TIMESTAMP&gt;
	&lt;/BODY&gt;
&lt;/NOTIFICATION&gt;</pre>
<p>When an MMS delivery report is received the system will generate a Postback notification. Not all carriers provide MMS delivery receipts.</p>
<pre>&lt;NOTIFICATION ID=&#8221;326&#8243; CREATED=&#8221;2011-08-02 07:20:52.332193-04&#8243;&gt;
	&lt;ORIGIN&gt;MMS_MT&lt;/ORIGIN&gt;
	&lt;CODE&gt;N102&lt;/CODE&gt; 
	&lt;BODY&gt; 
	&lt;HISTORYID&gt;249687&lt;/HISTORYID&gt; 
	&lt;MMSID&gt;35674&lt;/MMSID&gt; 
	&lt;TO&gt;16501234123&lt;/TO&gt; 
	&lt;TRACKINGID&gt;MMS_12346&lt;/TRACKINGID&gt; 
	&lt;SPID&gt;000189&lt;/SPID&gt; 
	&lt;HANDSET&gt;motol7c&lt;/HANDSET&gt; 
	&lt;STATUS CELLY=&#8221;20&#8243; PROVIDER=&#8221;1000&#8243; TEXT=&#8221;Retrieved&#8221; DESCRIPTION=&#8221;" /&gt; 
	&lt;TIMESTAMP&gt;2011-08-02 07:20:49-04&lt;/TIMESTAMP&gt; 
	&lt;/BODY&gt; 
&lt;/NOTIFICATION&gt;</pre>
