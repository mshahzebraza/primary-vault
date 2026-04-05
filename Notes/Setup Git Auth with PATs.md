---
original_path: Notes/Tech Learning/linux-pc-setup/Setup Git Auth with PATs.md
base: TechLearning
path_area: linux-pc-setup
categories:
  - "[[TechLearning]]"
  - "[[linux-pc-setup]]"
---
### Setting up the repo
When you clone a repository from github into your file-system, it automatically sets the upstream remote-url for the cloned repo. This remote-url is the way for git to know where is the remote repo located and uses this info to establish connection to it when you run commands like `git pull`, `git push` etc.

If you downloaded the manually, e.g. using the zip file, you'd need to set the remote url yourself. The command used to do it is as follows:
```sh
git remote set-url origin <link-to-your-remote-repos-git-file>
```

the `.git` file is located at the root level of your remote repository address. To get this you can simply visit the remote repository's web URL and append the `.git` to it. 

For instance,
```
https://github.com/[some-owner]/[some-repo].git`
```

However, after you've set up the repository's remote URL. You'll still need to authenticate each time you establish connection using commands like `git pull`. You can't use your Github password as its support is not removed.

### Authentication

The way I've used is to create a Personal Access Token (PAT) from `Github Settings > Developer Settings > Personal access tokens > Tokens (classic)`
or, if you can't find the settings page, visit the following URL

```
https://github.com/settings/tokens
```


There you can click "**Generate new token**". You'll be asked to provide some access permissions and an expiry date.

> I didn't know much about it and just checked all permissions with no-expiry-date.

Once you have the access-token, you must save it somewhere safe on your machine.
With this token, you can now successfully authenticate to use the git commands i.e. `git pull`.

Now when you run `git pull`, you can paste this token as a password.

### Configuration

However, pasting the token again and again is a bit of nuisance. To bypass this, you can permanently set it to your remote URL and git will always use the token from the configured remote URL to access the remote repo.

So, if earlier your remote repository was this:
```
https://github.com/[some-owner]/[some-repo].git`
```

now it should be this:

```
https://<your-github-access-token>@github.com/[some-owner]/[some-repo].git
```

To achieve this you can run the `set-url` command again.

```sh
git remote set-url origin https://<your-github-access-token>@github.com/[some-owner]/[some-repo].git
```

And you're all done. Now you can communicate with the remote repository without having to provide the PAT again and again.


## Other Methods

1. Another way is to setup the username and email in the global git config and then instead of hard-coding the PAT in the remote-URL of the local git config, just set the git config to cache the password. Watch [this video for further context](https://www.youtube.com/watch?v=kHkQnuYzwoo) 