# MailWebsiteChanges

Python script to keep track of website changes; sends email notifications on updates and/or also provides an RSS feed

To specify which parts of a website should be monitored, <b>both XPath selectors</b> (e.g. "//h1") <b>and regular expressions can be used</b>.

## Configuration
Configuration can be done by creating a <code>config.py</code> file (just place this file in the program folder):
Some examples:

### Website definitions
<pre>
<code>
 sites = [

          {'shortname': 'mywebsite1',
           'uri': 'http://www.mywebsite1.com/info',
           'type': 'html',
           'xpath': '//h1',
           'regex': '',
           'encoding': 'utf-8'},

          {'shortname': 'mywebsite2',
           'uri': 'http://www.mywebsite2.com/info',
           'type': 'html',
           'xpath': '//*[contains(concat(\' \', normalize-space(@class), \' \'), \' news-list-container \')]',
           'regex': '',
           'encoding': 'utf-8'},

          {'shortname': 'mywebsite3',
           'uri': 'http://www.mywebsite3.com/info',
           'type': 'text',
           'xpath': '',
           'regex': 'Version\"\:\d*\.\d*',
           'encoding': 'utf-8'}

         ]
</code>
</pre>

 * shortname
     + short name of the entry, used as an identifier when sending email notifications
 * uri
     + URI of the website
 * type
     + content type of the website, e.g., 'xml'/'html'/'text'
 * xpath
     + XPath expression. Set this to '' if you don't want to use it.
 * regex
     + Regular expression. Set this to '' if you don't want to use it.
 * encoding
     + Character encoding of the website, e.g., 'utf-8'.

<em>SelectorTest.py</em> might be useful in order to test the definitions before integrating them into the config file.

### Mail settings
<pre>
<code>
 subjectPostfix = 'A website has been updated!'
 sender = 'me@mymail.com'
 smtphost = 'mysmtpprovider.com'
 useTLS = True
 smtpport = 587
 smtpusername = sender
 smtppwd = 'mypassword'
 receiver = 'me2@mymail.com'

 os.chdir('/path/to/working/directory')
</code>
</pre>

If <em>receiver</em> is empty, no mail will be sent.


### RSS Feeds
If you prefer to use the RSS feature, you just have to specify the path of the feed file which should be generated by the script (e.g., rssfile = 'feed.xml') and then point your webserver to that file. You can also invoke the FeedServer.py script which implements a very basic webserver.

<pre>
 <code>
  rssfile = 'feed.xml'
  maxFeeds = 100
 </code>
</pre>


### Cron job
To setup a job that periodically runs the script, simply attach something like this to your /etc/crontab:
<pre>
 <code>
  0 8-22/2    * * *   root	/usr/bin/python /path/to/MailWebsiteChanges/MailWebsiteChanges.py
 </code>
</pre>
This will run the script every two hours between 8am and 10pm.


## Requirements
Requires <a href="http://lxml.de/">lxml</a>.

