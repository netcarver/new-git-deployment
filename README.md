Automate the creation of a deployment repo + hub on a single box.

Based on an idea from http://joemaller.com/990/a-web-focused-git-workflow/


Usage
=====

new-git-deployment <name>

Creates a new deployment directory, and initialises a full git repo in it. 
Then it creates a local deployment hub directory for it and initialises a bare git repo in it. This will be used as a remote for the development repos and allows them to push (being bare) to it.

The hub is also added as a remote of the full deployment directory and the two are tied together with some post-*
scripts.
