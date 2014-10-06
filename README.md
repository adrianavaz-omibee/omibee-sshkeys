# Omibee SSH Keys
Omibee engineers and technical people should add their SSH public keys to
the ssh directory of this project. These keys are periodically copied to
our Delivery systems.

# Creating Keys
```bash
ssh-keygen -b 4096 -f .ssh/id_rsa -C first.last@omibee.com -o -a 500
```

# Adding Keys
Keys should be added to the `ssh/` directory of this repository. Add your public key as `username.pub`, and then append it to `authorized_keys`. This might look something like:

```bash
# Be sure to replace SSHKEY_DIR and USERNAME with the correct values!
export SSHKEY_DIR=ssh
export USERNAME="username"

cd omibee-sshkeys/
cp ~/.ssh/id_rsa.pub ${SSHKEY_DIR}/${USERNAME}.pub
cat ${SSHKEY_DIR}/${USERNAME}.pub >> ${SSHKEY_DIR}/authorized_keys
```

Once your pull request has been merged into the master branch, the keys will
automatically be copied to all of the hosts using this script.


# Usage
SSH access can be granted using this process.

If the host has a cron that uses `/etc/cron.hourly/` then simply copy the
script into `/etc/cron.hourly/` like this:

```bash
cd /etc/cron.hourly/
curl -O https://bitbucket.org/omibee/omibee-sshkeys/raw/master/manage_authorized_keys
chmod +x manage_root_authorized_keys
```

If the cron on the system does not support `cron.hourly`, the following
crontab entry may be used.

```bash
mkdir -p /usr/local/bin
cd /usr/local/bin
curl -O https://bitbucket.org/omibee/omibee-sshkeys/raw/master/manage_authorized_keys
chmod +x manage_authorized_keys
crontab -e
```

The entry should look like:

```
# min hour dom month dow command
59 * * * * /usr/local/bin/manage_authorized_keys
```

# Inspired by
https://github.com/puppetlabs/puppetlabs-sshkeys