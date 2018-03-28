# CWDS Code Branching Approach

This is current default practice for our branching strategy:

* We favor [trunk based](https://trunkbaseddevelopment.com) development to enable CI/CD.
* Feature branches are used, but should generally not live past a single sprint.
* Releases are simply tagged as a commit on the master branch.
* Release branches are created if needed to fix bugs in production but should be as short-lived as possible as this is an exception process.
