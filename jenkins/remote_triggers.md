## How to remote remotely trigger Jenkins
### Create user
* Login to Jenkins
* Manage Jenkins -> Manage Users -> Create User

### Allow user to build/discover/read
* Login to Jenkins
* Manage Jenkins -> Configure Global Security
* User/group to add
* Enable: Overall read, Job build/discover/read
* Save

### Get API token for user
* Logout of Jeknins
* Login to Jenkins as user
* People -> USER -> Configure -> Show API Token

### Enable job for remote trigger
* Login to Jenkins
* Job -> Configure > check "Trigger builds remotely" -> Add
* "Authentication Token" -> Save

### Curl example
```
JENKINS_URL=""
JOB=""
USER=""
TOKEN=""
JOB_TOKEN=""
PARAMETERS=""
```

#### Regular Build
`curl --user ${USER}:${TOKEN} ${JENKINS_UR}/job/${JOB}/build?token=${JOB_TOKEN}"`

#### Build with parameters
`curl --user ${USER}:${TOKEN} ${JENKINS_URL}/job/${JOB}/buildWithParameters -d "token=${JOB_TOKEN}&${PARAMETERS}"`
