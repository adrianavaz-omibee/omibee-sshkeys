# Omibee SSH Keys
Omibee engineers and technical people should add/remove their SSH public keys to
the ssh directory of this project.

# Creating Keys
```bash
ssh-keygen -b 4096 -f .ssh/id_rsa -C first.last@omibee.com -o -a 500
```

# Adding Keys
Keys should be added to the `ssh/` directory of this repository. Add your public key as `username.pub`.

Afterwards, add your `username` to the `omibee_users`array in the `users.yml` file.

Once your pull request has been merged into the master branch, the users in `omibee_users` will be created in our managed servers and their keys added to their home directory `.ssh/authorized_keys`.

#Removing Keys
The inverse of "adding keys" should be done. This way we ensure that users are removed from our managed servers.

# SSH access to the Jump server and MFA setup
On your first SSH access to the jump server after adding your SSH keys, you will be prompted to configure MFA access.
The following procedures assume your public key and user have already been added to the server.

For that you will need a smartphone with an MFA app such as [Authy](https://www.authy.com/) ( [iOS](https://itunes.apple.com/en/app/authy/id494168017?mt=8) | [Android](https://play.google.com/store/apps/details?id=com.authy.authy&hl=en)).
Please install it on your phone before proceeding.

#### Steps to setup MFA:
 1. Open a terminal and SSH into the Jump server, ie, `ssh username@jump.omibee.com`
 2. (optional) confirm your RSA key via password if needed.
 3. When asked `Do you want authentication tokens to be time-based (y/n)`, reply `y`
 4. Using Authy (or equivalent app), scan the QR code that shows up on the screen.
 5. Follow the procedures on your smartphone to finish configuring Authy.
 6. Back on the SSH session, when asked `Do you want me to update your "~/.google_authenticator" file (y/n)`, reply `y`
 7. Keep answering `y` to all the following questions.
 8. You're done! :)

 From this point onward, everytime you SSH into (or through) the Jump server, you will be asked for a verification code.
 Open Authy on your smartphone and use the token for the Jump server indicated in the app.
