# tat-commit-msg
git commit-msg hook to send commit to TAT. 

Each commit will be a changelog entry in a topic 
using the [Release View](https://github.com/ovh/tatwebui-plugin-releaseview).

## Prerequisites
* [tatcli](https://github.com/ovh/tatcli) >= 0.56.1
* A [Tat WebUI](https://github.com/ovh/tatwebui) server with the [Release
  View](https://github.com/ovh/tatwebui-plugin-releaseview)

## Install

Download and copy `commit-msg` to your git repository hook folder:

```
sh-4.2$ cd my_git_repo
sh-4.2$ cd .git/hooks
sh-4.2$ wget https://raw.githubusercontent.com/cdumay/tat-commit-msg/master/commit-msg -O commit-msg
sh-4.2$ chmod +x commit-msg
```

## Configuration

### Using environment variables

This hook uses the following environment variables:
* `TAT_TOPIC`: The TAT topic to use.
* `TAT_VERSION`: Your software release.

```
sh-4.2$ export TAT_TOPIC=/Internal/Test
sh-4.2$ export TAT_VERSION=0.5
```

### Using files
This hook can load his configuration using the files in the git repository:
* `TOPIC`: The TAT topic to use.
* `VERSION`: Your software release.

```
sh-4.2$ cd my_git_repo
sh-4.2$ echo "/Internal/Test" > TOPIC
sh-4.2$ echo "0.5" > VERSION
```
## Example of use

```
sh-4.2$ cd my_git_repo
sh-4.2$ git commit -am "feat: This is a test with a jira link (#TEST-1)"
[tat /Internal/Test] New release '0.5' was created
[tat /Internal/Test] Changelog sent to TAT
[master db6ef2b] feat: This is a test with a jira link (#TEST-1)
 1 file changed, 1 insertion(+), 1 deletion(-)
```

**Result in Tat WebUI**

![Release View](https://raw.githubusercontent.com/cdumay/tat-commit-msg/master/view.png)

## Disable the Hook
The hook can be disabled by setting the environment variable `SEND_TO_TAT`

```
sh-4.2$ export SEND_TO_TAT=NO
sh-4.2$ cd my_git_repo
sh-4.2$ git commit -am 'feat: This is a usefull commit'
[tat /Internal/Test] TAT is disabled
[master bd2b6d7] update
 1 file changed, 1 insertion(+), 1 deletion(-)
```

**Note**: To reactivate the hook, just unset the environment variable `SEND_TO_TAT`
or set it to `YES` (or `Y`).

