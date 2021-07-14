# kit
## A git wrapper to teach Trunk-Based Development

### Why?

`kit` was built as a tool to teach principles of Trunk-Based Development (TBD). It is a bash script that wraps git to provide only the commands necessary for TBD, as simply as possible, in a way to encourage thinking in a continuous integration mindset.

`git` is a very powerful SCM, with an arcane UI. The vast majority of its features are arguably unnecessary, especially for TBD, and especially for a beginner learning TBD. `kit` is intended to remove the distractions, and simplify the interaction with git, so that the focus can be on the concepts of TBD.

### Why not?

`kit` is not a long-term replacement for `git`. In theory any developer practicing TBD _could_ use `kit`, but this is neither the intention nor the recommendation. There is value in getting to grips with `git`.

### Usage

To make an existing `git` repo ready for using `kit`, run:

    kit init

in the root of the repo. This will create the `.kit` metadata directory which you may wish to add to your `.gitignore`.

Before making a change, run `begin` and enter a description for the change:

    $ kit begin
    What is the change you wish to make?
    Implement fetching user by email address
    
Asking the developer to right the change message in advance is by-design - it forces changes to be more deliberate and focussed, in contrast to the git model of writing the commit message at the end.

After a `kit` change has begun, running `kit current` at any time will display the message.

Once all changes have been made, they may be integrated by running the `integrate` command:

    $ kit integrate
    TODO no feedback on change being integrated!!!
    
This will fetch any changes that teammates have made in the meantime, as well as pushing local changes to the remote repo. If there have been remote changes, these will be listed so that the developer is aware of what they are integrating with - this is an important part of TBD, being aware of the changes made by teammates, so that you can adapt to them, learn from them, and provide feedback on them.

If there is a conflict with incoming changes, this will need to be resolved by changing the affected files and continuing to run `kit integrate` until there are no more conflicts.

    $ kit integrate
    There are conflicts with an incoming change - please resolve these then re-run 'kit integrate'
    [...change conflicting files...]
    $ kit integrate
    TODO feedback!

To back out of an in-progress change, run the `backout` command:

    $ kit backout
    TODO feedback!
    
This will revert all local changes, and also integrate any remote changes so that the local copy is as up-to-date as possible before beginning another change.

That's it.
 
### Installation

Place `kit` somewhere on your `PATH`. A `git` installation is a prerequisite.

### Contributing

I am happy if anybody using this wishes to fix bugs or suggest changes - please open a github issue on the project with an appropriate level of detail, and optionally a pull request referencing the issue.

Please take care, if you are making code changes, to at least run the `./test` script to ensure nothing is broken and update it to cover the changes you make. I personally use the script to TDD changes here, but would not (cannot!) force you to do that.

Before suggesting adding new commands, be sure they fit with the philosophy of the project (see the "Why?" section above).