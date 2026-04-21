
# General FAQs

Find answers to some of the most frequently asked general questions.

## Training

### Is there a training outline?

An end-to-end course can be found at [XMPro Courses](https://courses.xmpro.com/course-library/). It is broken down into 17 lessons - totaling 7 hours - covering an overview, Data Stream Designer, Recommendations, and App Designer.

You can also find an extensive array of YouTube videos on various topics of interest on our YouTube channel [XMPro learning](https://www.youtube.com/channel/UCSnVNXaDqVizaoZHPjKhwRA).

### Are there any prerequisites for the training?

As XMPro is a no-code platform, there are no technical prerequisites.

We do recommend the following to make your training more effective:

* Start with a Use Case/problem statement in mind
* Have access to an XMPro instance so you can practice and work out issues

## Session Timeout

### How does the XMPro sign-in process work?

1. When you try to sign in to XMPro Data Stream Designer or App Designer, you're redirected to the linked XMPro Subscription Manager's sign-in page.
2. Enter your username and password to log in.
3. Upon signing in, you receive credentials as browser cookies for both Subscription Manager and the site you wish to access.
4. Subscription Manager redirects you back to the requested site, granting you an access token using those cookie credentials.
5. The access token is valid for the duration specified in the site's Session Timeout setting, while cookies last for longer periods (e.g., an hour).

Cookies enable access to the website's pages and assets like JavaScript and images, while the access token allows you to access the site's data, which is essential for activities like navigating, viewing live updates on app pages and saving changes.

> [!NOTE]
> The Session Timeout setting is accessible by the Site Admin and can be found in Subscription Manager under the details blade for the product (e.g., App Designer).

### How long do I stay signed in?

* Without "Remember Me": you stay signed in for 1 hour or until your browser session ends (e.g. closing the browser window).
* With "Remember Me": you stay signed in for 30 days or until the site is unable to silently refresh the credentials.

> [!NOTE]
> The Remember Me checkbox can be found when signing into XMPro.

### How does the Silent Refresh functionality work?

When using XMPro App Designer, Data Stream Designer, or Subscription Manager, the site attempts a silent refresh of the credentials as the access token nears its expiry time.

If successful, a new token is granted, valid for the duration specified in the Session Timeout setting.

If unsuccessful, the site displays a login expired warning with a prompt to sign in again. Clicking the button redirects you to Subscription Manager for credentials.

If the Subscription Manager cookie is still valid, it automatically issues a new access token and redirects back to the original site; otherwise, you're prompted to sign in again.

Successful attempts through either path will refresh the cookie credentials if they're nearing expiry and meet refresh conditions.

Refreshing the page will also update the credentials.

## Versioning

### What version of XMPro am I using?

Whether you are logging a support issue or looking for a specific product feature, knowing the version of the XMPro Platform you're using is important.

Click the help icon top right of the web applications to view the help blade. It contains the version number as well as helpful links such as release notes and logging a support ticket.

From v4.4.4 onwards, you can access more details in the following ways:

For web applications only, check the `/version` endpoint, which produces a response such as...

```json
{
  "ApplicationTitle": "XMPro App Designer",
  "XMProPlatformVersion": "4.4.4",
  "InformationalVersion": "4.4.4.28+8c9912b045",
  "GitCommitId": "8c9912b04592ac2d54bf4fa9a522203cbd21bc98",
  "GitCommitDate": "2024-05-10T04:41:02Z"
}
```

For all applications, check the log files. On application start, a log event like the following will be generated.

```log
[12:00:00.123] [Information] [XMPro.Runtime.Runtime] 
  Running "XMPro Stream Host" "4.4.4.33+bc71a3ebfc" on "Ubuntu"
  [RuntimeInfo] RuntimeInfo {
    Title = XMPro Stream Host,
    XMProPlatformVersion = 4.4.4,
    AssemblyInformationalVersion = 4.4.4.33+bc71a3ebfc,
    GitCommitId = bc71a3ebfc82632d60586503878e8867fbf2e0b4,
    GitCommitDate = 2024-05-13T07:10:29Z 
  }
