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