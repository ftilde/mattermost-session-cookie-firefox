# mattermost-session-cookie-firefox

mattermost-session-cookie-firefox is a script to obtain the session cookie from
a mattermost webclient. It is designed to be used with the `tokencmd`
configuration option of
[matterhorn](https://github.com/matterhorn-chat/matterhorn) for mattermost
instances that do not allow username/password or personal access token login.

## Depencencies
* `/bin/sh`
* firefox
* curl
* sqlite3

## Usage
```
$ mattermost-session-cookie-firefox
Usage: mattermost-session-cookie-firefox HOST [PROFILE]
```

To use the script with firefox, add this script to your `$PATH` and something
like the following to your matterhorn `config.ini`:
```
tokencmd: mattermost-session-cookie-firefox my.mattermost.host.com my-firefox-profile-name
```

## How it works
First, the cookie file for the provided or otherwise the first found firefox
profile is located. Then, it is tried to extract the value of the `MMAUTHTOKEN`
cookie for the desired host and if that succeeds, a test api call to the
specified host is made. If the cookie is present and the api call succeeds, the
cookie value is printed to stdout. Otherwise, a webpage is opened in the
browser (firefox) which asks the user to log in using the webclient of the
mattermost instance. In the meantime, the above cookie retrieval and check
procedure is repeated until it succeeds.
