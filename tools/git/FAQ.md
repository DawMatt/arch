# Frequently Asked Questions

# How do I add SSH to my GitHub account?

A: Steps

* Create your ssh key if you don't already have one
* Binary copy your public key to clipboard:


Windows:
```
clip < ~/.ssh/id_rsa.pub
```
Mac:
```
pbcopy < ~/.ssh/id_rsa.pub
```
* [GitHub page: Adding a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

# How do I create Personal Access Tokens for use with HTTPS?

A: Steps:

* Go to https://GitHub.com/settings/tokens to crete a token. Note: this URL can be adapted to work with GitHub Enterprise sites.
* [GitHub Page: Creating an Access Token for command-line use](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)
* Make a copy of your token in a safe place. You'll use this token as your password.

# Which Git credentials should you use with tools when using HTTPS while Two Factor Authentication is active?

A: Your standard username, and a personal access token instead of the password. For more detail see:
* [Github page: Remote URLs](https://help.github.com/en/articles/which-remote-url-should-i-use)
* [Github page: Credential helper](https://help.github.com/en/articles/caching-your-github-password-in-git)

