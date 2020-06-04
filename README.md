# Mattermost Zoom Plugin 

[![Build Status](https://img.shields.io/circleci/project/github/mattermost/mattermost-plugin-zoom/master)](https://circleci.com/gh/mattermost/mattermost-plugin-zoom)
[![Code Coverage](https://img.shields.io/codecov/c/github/mattermost/mattermost-plugin-zoom/master)](https://codecov.io/gh/mattermost/mattermost-plugin-zoom)
[![Release](https://img.shields.io/github/v/release/mattermost/mattermost-plugin-zoom)](https://github.com/mattermost/mattermost-plugin-zoom/releases/latest)
[![HW](https://img.shields.io/github/issues/mattermost/mattermost-plugin-zoom/Up%20For%20Grabs?color=dark%20green&label=Help%20Wanted)](https://github.com/mattermost/mattermost-plugin-zoom/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22Up+For+Grabs%22+label%3A%22Help+Wanted%22)


**Maintainer:** [@larkox](https://github.com/larkox)
**Co-Maintainer:** [@mickmister](https://github.com/mickmister)

Start and join voice calls, video calls and use screen sharing with your team members via Zoom.

Usage
-----

Once enabled, clicking the video icon in a Mattermost channel invites team members to join a Zoom call, hosted using the credentials of the user who initiated the call.

![Screenshot](https://user-images.githubusercontent.com/177788/42196048-af54d2b8-7e30-11e8-80a0-5e160ae06f03.png)


Zoom Setup Guide
-----

You will need a paid Zoom account to use the plugin.

1. Go to **System Console > Plugins > Zoom** to configure the Zoom Plugin.

![image](./assets/settings.png)

2. If you're using a self-hosted private cloud or on-premise Zoom server, enter the **Zoom URL** and **Zoom API URL** for the Zoom server, for example `https://yourzoom.com` and `https://api.yourzoom.com/v2` respectively. Leave blank if you're using Zoom's vendor-hosted SaaS service.

3. Set the **API Key** and **API Secret**, generated by Zoom and used to create meetings and pull user data:

  - Go to https://marketplace.zoom.us and log in.
  - In the top left click on **Develop** and then **Build App**.
  - Enter a name for your app and disable **Intend to publish this app on Zoom Marketplace**.
  - Choose **Account-level app** as the app type.
  - Select **JWT API Credentials** as authentication type.
  - Click **Create**.
  - Enter the **Company Name** and **Developer Contact Information** for your app.
  - Go to the **App Credentials** tab on the left. Here you'll find your **API Key** and **API Secret**.
  - Paste the **API Key** and **API Secret** into the fields in the System Console, and hit **Save**.
  
![create app screen](https://github.com/mattermost/docs/raw/master/source/images/zoom_api_key.png)

To generate a working **API Key** and **API Secret** a [Pro, Business, Education, or API Zoom plan](https://zoom.us/pricing) is required.

4. Set the **OAuth ClientID** and **OAuth Secret**, generated by Zoom and used to create meetings and pull user data:

  - Go to https://marketplace.zoom.us/ and log in.
  - In the top left click on **Develop** and then **Build App**.
  - Select **OAuth** in **Choose your app type** section.
  - Enter a name for your app and disable **Intend to publish this app on Zoom Marketplace**.
  - Choose **Account-level app** as the app type.
  - Click **Create**.
  - Enter the **Company Name** and **Developer Contact Information** for your app.
  - Go to the **App Credentials** tab on the left. Here you'll find your **Client ID** and **Client Secret**.
  - Enter a Valid **Redirect URL for OAuth** (`https://<SiteUrl>/plugins/zoom/oauth2/complete`) and add the same url under **Whitelist URL**.
    * `SiteUrl` should be your mattermost server url
  - Add following scopes "user:read", "meeting:write", "webinar:write", "recording:write"
  - Paste the **Client ID** and **Client Secret** into the fields in the System Console, and hit **Save**.
  - Generate an **Encryption Key** to save the encryped tokens.

![create OAuth app scrren](./assets/oauth_creds.png)


5. Enable settings for [overriding usernames](https://docs.mattermost.com/administration/config-settings.html#enable-integrations-to-override-usernames) and [overriding profile picture icons](https://docs.mattermost.com/administration/config-settings.html#enable-integrations-to-override-profile-picture-icons).

6. Activate the plugin at **System Console > Plugins > Management** by clicking **Activate** for Zoom.

![image](https://github.com/mattermost/docs/blob/master/source/images/zoom_system-console_management.png)

Once activated, you will see a video icon in the channel header. Clicking the icon will create a new Zoom meeting, and create a post with a link to the meeting. Anyone in the channel can see the post and can join by clicking on the link.

![image](https://user-images.githubusercontent.com/177788/42196048-af54d2b8-7e30-11e8-80a0-5e160ae06f03.png)

Note
----
   Users will need to sign-up for their own Zoom account using the same email address that they use for Mattermost. If the user attempts to start a Zoom meeting without a Zoom account, they will see the following error message: "We could not verify your Mattermost account in Zoom. Please ensure that your Mattermost email address matches your Zoom email address."
   In addition, the user must be added to the admin's Zoom account to quickly start a meeting without having to share a personal meeting ID.


## Development

This plugin contains both a server and web app portion.

Use `make dist` to build distributions of the plugin that you can upload to a Mattermost server for testing.

Use `make check-style` to check the style for the whole plugin.

### Server

Inside the `/server` directory, you will find the Go files that make up the server-side of the plugin. Within there, build the plugin like you would any other Go application.

### Web App

Inside the `/webapp` directory, you will find the JS and React files that make up the client-side of the plugin. Within there, modify files and components as necessary. Test your syntax by running `npm run build`.
