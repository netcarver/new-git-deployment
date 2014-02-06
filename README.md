New Git Deployment Script
=========================

This script automates the creation of a 'prime' deployment repository and a linked, bare, 'hub' repository on a single
box.

It's based on an idea from [A Web Focused GIT Workflow](http://joemaller.com/990/a-web-focused-git-workflow/) and can be
used either to setup things as presented in that paper or with just one-way replication from 'prime' to 'hub'. I find
the later scenario useful for automatic backups of my local development repositories.


Environment Variables & Customisation
-------------------------------------

You can configure the root for both your hubs and primes using the environment variables ```NGD_HUB_ROOT``` and
```NGD_PRIME_ROOT``` respectively (probably in your ```.bashrc``` file.) If you don't setup these variables then all the
hubs will be created as ```~/.live-hub/<repo-name>.git``` and the primes will appear as ```~/live/<repo-name>/```
directories.

If you are using your hubs as backup repos then you could use something like sshfs to mount a remote share and have the
mountpoint as your ```NGD_HUB_ROOT```.

If you only ever want to create 'prime' to 'hub' replication then you can set the ```NGD_OPTION``` environment variable
to ```--one-way```.


Usage
-----

To create a new, empty, full 'prime' and bare 'hub' repository with bi-directional sync:

    new-git-deployment <repo-name>

Replace ```<repo-name>``` with the name of your project. These can be on your deployment server and you can then just
clone the hub to your local development machine to get started and add the hub as a remote.


To create a new, empty, full development 'prime' and bare backup 'hub' repository with only prime to hub sync:

    new-git-deployment <repo-name> --one-way

You then work locally in your project's prime directory and all your commits will get reflected to your backup 'hub'
repo. This can be controlled by the ```NGD_OPTION``` environment variable if this is the only scenario you ever use.


You can also have your project be a clone of another git repository by supplying the existing project as an argument...

    new-git-deployment <repo-name> <uri-of-repo-to-clone> [--one-way]

