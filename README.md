# Cloud Code Guestbook Sample - REMOTE EDITION

This is a quick experiment to see how easily our Cloud Code extension works w/ the newly announced [Remote Development](https://code.visualstudio.com/blogs/2019/05/02/remote-development) Support in VS Code.

## What's the point
Several things are cool here:
1. A user to fire up the sample with minimal set-up steps
2. Images can be maintained of a fully configured set-up
3. Where a new developer machine is required the dockerfile makes it's set-up repeatable
4. You can conceptually run the container anywhere 

But the bottom line is a simple repo like this can not only contain the app you are working on and the K8s artifacts to deploy it.  But it can also contain the required declarative artifacts to set up your developer machine.

## Pre-reqs
To get this to work you need:
1. Latest [VS Code Insiders](https://code.visualstudio.com/insiders/) 
2. Git (you could download the tar but...)
2. Docker Desktop

However that should be it - no other tools are required on your local machine.

## QuickStart

### Git clone the repo and open VS Code Insiders
```bash
git clone https://github.com/seanmcbreen/remote-guestbook.git
cd remote-guestbook
code-insiders .
```

### When promoted to re-open as a container say `Reopen in Container`

![re-open](README-Images/remote.png)

### The container will be built [takes a few minutes the first time only] and you can see the details but clicking `details`.

![details](README-Images/details.png)

When finished it will look like:

![finished](README-Images/finished.png)

### Log-into GCloud via the Cloud Code GKE explorer (you can also do via CLI and this could be part of the docker file as well).

![log-in](README-Images/login.png)

Follow the prompts in the terminal.

OK you are done - everything e.g. `Continuous Development` and `Cluster Exploration` and `Debugging` should just work.  But remember none of the required tools for that are on your machine e.g. no `GCloud` or `Kubectl` or even the extension.

## What is in the image
The [dockerfile](https://github.com/seanmcbreen/remote-guestbook/blob/master/.devcontainer/Dockerfile) for the remote development host does a few things.  Specifically it adds in the toolchain required for our project and the extension:

1. Latest `node:lts` image
2. Add the `cloud code` and `docker` extensions
3. Adds `npm`, `typescript` and `tslint`
4. Installs `git`
5. installs `Docker CE`
6. installs `GCloud` and `kubectl`
7. Installs `skaffold`
8. installs `helm`

This takes the requirement away form the user to do any of these things.

## Known issues

* I hard coded my image registry `seanmcb-test` as the default for Skaffold.
* You have to manually log-into `GCloud`
* I hard coded the version of `GCloud` to get.
