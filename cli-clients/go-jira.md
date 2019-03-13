[go-jira](https://github.com/Netflix-Skunkworks/go-jira)
---------

Simple command line client for Atlassian's Jira service written in Go written by Netflix.

This setup is geared towards OSX.

## Install
```
brew install go-jira
```

## Auth
Since we use a hosted Jira instance we need and API token:

### [Steps to get API token](https://confluence.atlassian.com/cloud/api-tokens-938839638.html?_ga=2.12700919.1355502723.1551978477-867772758.1550521990)
* Go to [url](https://id.atlassian.com/login)
* Login with Jira creds
* Go to `Security` tab
* Click `Create and manage API tokens` link
* Click `Create API Token` button
* Provide a label/name in the popup -> click create
* Copy token to clipboard and save some place safe

## Configure
You will need to following info:
- [ ] JIRA_URL
- [ ] JIRA_USER
- [ ] Your password/token

* Create `~/.jira.d/config.yml` if not already there
* Add:
  ```
	password-source: keyring
	endpoint: JIRA_URL
	user: JIRA_USER
	person: JIRA_USER@spreedly.com
	```

## Test
Use `jira session` to test your config and api key/password. Note that after the first prompt for your api key/password, it will be stored in the OSX keyring.
  ```
	$ jira session
	? Jira API-Token [JIRA_USER]:  [? for help] ************************
	op: Get
	url: JIRA_URL/rest/auth/1/session
	err: {}
  ```
	
## Useful commands
### My open tickets
```
jira list -q 'assignee = currentUser() AND resolution = Unresolved order by updated DESC'
```
