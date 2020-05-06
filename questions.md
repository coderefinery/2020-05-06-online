

## Questions, answers, and feedback

### Working with remotes

- For me `git branch` shows the same output as `git branch --list`
  - Same for me (I did not know `git branch --list`). I personally use
    `git branch` to see local branches that I only have locally, and
    `git branch -r` or `git branch --remote` to see remote
    branches. There is also `git branch -a` or `git branch --all` to
    see both local and remote branches.

- Difference between fork and pull? (and clone -- is that just to a
  local machine rather than also the GitHub userspace?)
  - Fork: copies the repository to your GitHub userspace where you
    have write permissions and can make changes. Fork is like a copy.
  - Pull: Fetches changes from a remote repository and merges them to
    your current local branch. We use `git pull` to update local
    repository with changes that happened in a remote repository. It
    is a 2 step process (fetch + update)
  - Clone: Copies the whole repository (all commits, all branches) to your 
    computer. This is the first step when starting to work on an existing 
    repository. After that synchronization with remote takes place via pull/fetch and push.

### Centralized workflow

- Is there a security advantage when using a SVN-like repository
  compared to a distributed git-repository? (As in not everybody owns
  the full history, or others?)

  - In svn you can have more finer control of read/write permissions,
    even per-folder.
  - This is why some companies prefer it, more control.
  - In Git if you have read permissions, you have read permissions to
    everything. Same for write permissions.
  - Disadvantage of SVN-like systems: single point of failure, you
    cannot save changes without network, and probably impossible to
    get contributions from external collaborators.

- I see groups can create their own github page that collects the
  group's GitHub repo, how can one do it? Will this be discussed in
  this lesson?
  - Yes one can create "GitHub organizations" for e.g. research groups
    or teams. Under this organization one can collect all the
    repositories for that group. Here's more info:
    https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/about-organizations

- Is it possible to see which git repos you have collaborator status
  on in your own github account? Or do you just have to remember which
  yourself?
  - https://github.com/settings/repositories

- Git gives you the chance to create a new pull request to revert
  changes from your previous pull request. Would you say that revert a
  PR is allowed as a best practice and, if so, when would it be useful
  to do it?
  - reverting a "bad PR" by a new PR is I think better than just
    "silently" undoing it in a commit to the main branch
  - exception is if someone accidentally commits sensitive
    information. In that case it's better to unprotect the main branch
    (if it was protected to begin with) and forcefully remove the
    commit with `git reset` (so that the sensitive information is lost
    forever and not still there in git history)

- As we did not finish completly in our room, I would like to ask: How
  can I submit something for the pull request?
   - by cloning a repository, creating a new branch and committing to
     it, and then pushing it, you can create a pull request. Either
     you go to the repository online, or you use the direct url link
     which is displayed in the output of the `git push` command
  - you can also create pull requests directly from the web by
    clicking the "pen" edit button and then propose a change which
    will create a fork and branch for you.

- Okay, a pull request is technically a whole process, not only the
  last step online?
  - yeah I think one can see it as a whole process. It can also be
    viewed as a step in a workflow, or that collaborating on a
    repository gravitates around making and reviewing Pull Request(s).

- And I let always others check to accept the pull request?
  - It is good practice to let somebody else review so we try to avoid
    reviewing our own changes (the same way we try to avoid reviewing
    our own papers). It is also a way to signal changes have happened
    to collaborators, and discuss the changes that have been made. At
    least two people then know about a change, instead of just one.

### Distributed version control and forking workflow

- Once this was accepted, my files/my changes are automatically
  transferred into the master branch? If done, I could delete my
  branch.
  - Yes, after accepting a pull request the branch (submitted in the
    PR) gets merged into the branch that the PR was submitted to. In the
    exercise we did that was the `master` branch. After merging PR, it's
    safe to delete the feature branch (PR = pull request :-)

- Why is it called a pull request? The admin of the repo has to pull
  the changes into the master branch?
  - name is for historical reasons since technically under the hood it
    is like "please pull from my branch to your branch". A better name
    is "merge request" (this is the name on GitLab). I like to think
    of it as "change proposal".

- I assume branches can have similar features of fork? When is it
  recommended to fork instead of branch?
  - Right. Forks add one layer: we can branch within a repository and
    then we can "branch" (fork) repositories. For a small group,
    working within one repository is typically easier. However, you
    need to fork if you want to make changes to repositories of others
    who do not know you. If I want to modify numpy, pandas, some
    library, I would have to start with a fork until the maintainers
    see my work and perhaps eventually add me as collaborator.
  - Forks can also help keeping branches in the "central" repository
    better organized.
  - Forks have really boosted open source software development since
    everybody can make changes in their userspace and propose changes.

- The lesson mentions about automated testing (test.py). Does
  coderefinery have a lesson on that which I can follow?
    - Yes we have: https://coderefinery.github.io/testing/
    - and we will hopefully give a workshop on May 18-20 which will
      cover testing, documentation, reproducible research, modular
      code development, etc.

- Missed the part regarding the time for reviewing. When does the time
  go up? Should one submit larger changes or rather smaller changes
  so it is easier for the gatekeeper to keep an overview?
    - In general smaller changes are easier to review and accept.
    - Usually changes are submitted when a feature is complete
      (regardless of the numbers of commits). Try to make a reviewer's
      job easier and keep the commits to a minimum and associated to a
      certain feature (e.g. changing a function and only that
      function).
    - Okay, but I can still do many commits on my side and send one
      overall commit with the pull request back? How is this realised?
      But I think he answered it, by checking out a new branch on my
      side.
        - You can, before pushing your commits, reorder, squash and
          even remove commits to make your branch's history more
          "readable". But that's more advanced topic; you can check
          `git rebase -i` for more.
        - To start with, it's perfectly ok to do many small commits in
          a feature branch and submit and review those. And remember
          to commit and push and review often.
           - Thank you, I would feel currently more comfortable to do
             a lot of smaller changes and keep track of them.
           
- What is a delta? What are resolving deltas?
    - Delta means all the differences between the local and the remote
      repository. Resolving deltas probably means git program
      internally chewing and processing to find out what are the
      differences to fetch them.

- What is fast forward?
  - a "fast forward" merge is where you merge branches without
    creating a merge commit by simply moving the branch pointer
    forward. This creates linear history rather than with branching
    points and merge commits

- Is fast forward same as rebase then?
  - the difference to rebasing is that fast-forward is only possible
    if merging can take place by simply moving the branch pointer
    forward in time. e.g. if the branch `featureA` is 4 commits ahead
    of `master`, and there are no new commits on master, merging can
    take place by "fast-forwarding" `master`
  - rebasing on the other hand replays the commits on top of the
    branch you're merging into. The commit hashes will in this case
    change
  - fast-forward merges are actually usually the default behaviour. 
    The instructor had a Git configuration set which made
    fast-forward merges *not default*, and needed to override it with
  - Here is little bit more about rebase vs. merge by Bjørn:
    https://coderefinery.org/blog/2020/04/24/rebase-vs-merge/ if you
    find it useful.

- When you pull from an upstream (central) repo, is a new branch then
  created in the local repo?
  - You typically pull into an existing branch. Git pull fetches
    changes from upstream and then merges them into your current
    (local) branch.

- I assume from the presentation that when we pull/fetch from
  upstream, it is merged to the master? What if I need to update a
  branch before making a pull request? Do I pull to the branch from
  the local (updated) master?
  - `git fetch` fetches commits that you do not have locally but does
    not modify any local branches
  - `git pull` fetches and modifies your current branch, which does
    not have to be `master`
  - To update a branch before making the pull request you can first
    update your local master, then merge that change to your local
    side-branch (or rebase the side-branch on top of master), then you
    can push that one and create a pull request.

