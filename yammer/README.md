NO LONGER SUPPORTED.

  

Sends build notifications to Yammer.

# Yammer Plugin for Jenkins

The Yammer Plugin for Jenkins enables notifications to be sent to a
Yammer group on the success or failure of a build.  
[Yammer Plugin on
jenkins-ci.org](https://wiki.jenkins-ci.org/display/JENKINS/Yammer+Plugin).

This is an example of a successful build notification sent to the
**Build Notifications** group:

![](https://raw.github.com/jenkinsci/yammer-plugin/49f2905714a463a290254c5603d30ff03a54e80f/readme/success_notification_in_yammer.png)

## Installation

### Easy install

Install the plugin from the Jenkins Plugin Manager. It should be listed
as **Yammer Plugin** under **Build Notifiers**.

### Manual install

-   Install the ruby-runtime plugin.

&nbsp;

-   Install the [Token Macro
    Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Token+Macro+Plugin).
    It may already be installed.

&nbsp;

-   Download the latest Yammer Plugin .hpi file from:
    <http://maven.jenkins-ci.org/content/repositories/releases/org/jenkins-ci/ruby-plugins/yammer>.

&nbsp;

-   Upload the .hpi file into Jenkins from Plugin Manager \> Advanced.

&nbsp;

-   Restart Jenkins.

## Obtaining an Access Token

See: [Obtaining an Access
Token](https://github.com/yammer/yam/blob/aa2a851db06d7821f7641c5557f925be42b0c2e5/README.md#obtaining-an-access-token)

## Enabling Yammer Notifications

In the job configuration, under Post-build Actions, select **Yammer
Notification**:

![](https://raw.github.com/jenkinsci/yammer-plugin/49f2905714a463a290254c5603d30ff03a54e80f/readme/enable_yammer_notifications_for_job.png)

The Access Token defaults to an environment variable named
YAMMER\_ACCESS\_TOKEN under the assumption that the same access token
will likely be the same for many, if not all jobs.  
For example, you might create a Yammer user representing Jenkins that
will act as the source of all Yammer notifications from Jenkins.

Global environment variables can be set from Jenkins at Manage Jenkins
\> Configure System \> Global Properties:

![](https://raw.github.com/jenkinsci/yammer-plugin/49f2905714a463a290254c5603d30ff03a54e80f/readme/oauth_environment_variables.png)

With the Access Token set, select whether to send success and/or failure
notifications:

![](https://raw.github.com/jenkinsci/yammer-plugin/49f2905714a463a290254c5603d30ff03a54e80f/readme/enable_success_notifications.png)

Both success and failure notifications require a message and a group
name. Environment variables are also allowed.

Please ensure that the Yammer user associated with the OAuth token has
been added to the specified groups,  
otherwise the post will result in a HTTP 403 Unauthorised error.

## Config File

The same settings specified in the job configuration can be provided as
a JSON file that can be generated during the build. By default, the file
should be named `yammer.json` under the workspace root.

Example file:

``` syntaxhighlighter-pre
{
    "success": {
        "message": "This success message was generated by the build.",
        "group": "Build Notifications"
    },
    "failure": {
        "message": "This failure message was generated by the build.",
        "group": "Build Notifications"
    }
}
```

The file path can be changed in the 'Advanced' section of the job
configuration.

Please note that the settings specified in the job configuration will be
merged with the config file. Any duplicate settings will overidden by
the config file.

## Support

[Raise an issue](https://github.com/jenkinsci/yammer-plugin/issues)

## Changelog

### Version 1.1.0 (July 19, 2013)

-   Add config file so that settings can be generated during the build.

### Version 1.0.0 (March 15, 2013)

-   Upgrade to OAuth 2.0 requiring only an access token.

&nbsp;

-   Yammer group name replaces group ID.

### Version 0.1.1 (March 15, 2013)

-   Add support for Jenkins version 1.505. Thanks [Jörg
    Wendland](https://github.com/jwendland).

&nbsp;

-   Use better OAuth terminology (consumer instead of client). Thanks
    [mikec-bullhorn](https://github.com/mikec-bullhorn).

### Version 0.1.0 (June 24, 2012)

-   Initial release.

Last updated: 2013-07-19 19:44:41 +1000