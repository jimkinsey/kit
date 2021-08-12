# kit
## A git wrapper to teach Trunk-Based Development

![Three kittens separated from their mother by a tree trunk bearing scratch marks](teaching-trunk-based-development.png)

`kit` is a tool to teach and demonstrate the value of trunk-based development. It's a fairly thin wrapper around git, providing a small, tailored, set of commands, that I cooked up one time when asked to work with some newly hired junior developers. That is probably all it's fit for - it can certainly work in any git repo, but has only been used in a fairly controlled scenario. Use at your own risk - but if you find anything to fix, feel free to contribute!

To make an existing `git` repo ready for using `kit`, `cd` to the root of the repo and execute

    $ kit init

This will create the `.kit` metadata directory which you may wish to add to your `.gitignore`

    $ echo ".kit >> .gitignore"

Before making a change, run `begin` and enter a description for the change:

    $ kit begin
    What is the change you wish to make?
    Implement fetching user by email address

Asking the dev to write the change message in advance is by-design - it forces changes to be more deliberate and focussed, in contrast to the git model of writing the commit message after the fact.

It's quite common to get started on a change and realise there are other changes you need to make first (often in the spirit of "make the change easy then make the easy change"). You can backout of your current work like so

    $ kit backout
    Backed out of:
    --------------
    Implement fetching user by email address

This will revert all local changes, and also integrate any remote changes so that the local copy is as up-to-date as possible before beginning another change. Backing completely out of a change in this situation might sound extreme, but again it is by design, to encourage smaller, more deliberate, easier-to-integrate, changes.

After a `kit` change has begun, running `kit current` at any time will display the description of the work in progress

    $ kit current
    Implement fetching user by email address

Once your change has been made, it may be integrated

    $ kit integrate
    Integrating
    -----------
    Implement fetching user by email address

This will fetch any changes that teammates have made in the meantime, as well as pushing local changes to the remote repo. If there have been remote changes, these will be listed so that the developer is aware of what they are integrating with - this is an important part of TBD, being aware of the changes made by teammates, so that you can adapt to them, learn from them, and provide feedback on them.

    $ kit integrate
    Integrating
    -----------
    Implement fetching user by email address
    
    Integrating incoming changes
    ----------------------------
    Fix email address validation

If there is a conflict with incoming changes, this will need to be resolved by changing the affected files and continuing to run `kit integrate` until there are no more conflicts.

    $ kit integrate
    Integrating
    -----------
    Implement fetching user by email address
    
    Integrating incoming changes
    ----------------------------
    Improve naming on user fetching API
    
    There are conflicts with an incoming change - please resolve these then re-run 'kit integrate'

    $ kit integrate
    Integrating
    -----------
    Implement fetching user by email address
 
### Installation

Place `kit` somewhere on your `PATH`. A `git` installation is a prerequisite.

### Contributing

I am happy if anybody using this wishes to fix bugs or suggest changes - please open a github issue on the project with an appropriate level of detail, and optionally a pull request referencing the issue.

Please take care, if you are making code changes, to at least run the `./test` script to ensure nothing is broken and update it to cover the changes you make. I personally use the script to TDD changes here, but would not (cannot!) force you to do that.

Before suggesting adding new commands, or changing existing ones, be sure it fits with the philosophy of the project!

#### Known improvements to make

 - `kit` only works in the root of the repo at present
 - the user feedback is awkward in places ("What is the change you wish to make?")
 - _possibly_ `kit current` should list changed files, like `git status`
 - test "framework" is home-baked, and probably half-baked. I am no bash expert, and there may be better / more standard ways to do this...
 - generally, the bash scripting could probably be improved...