Like everything else in this class, I had Claude+ on Poe provide these instructions for handling class assignments from here on out: 

# Here are the main steps for students to fetch assignments from your repo and submit pull requests:


    The students will first need to clone your repo to their local machine. They can do this by running:


```
git clone https://github.com/your-username/your-repo-name.git
```

###    Each week, they will need to fetch the latest changes from your repo, which will contain the new assignment. They can do this by running:

```
git fetch origin
```

###    Then they should check out the new assignment branch. For example, if the new assignment is on a branch called "assignment-3", they would run:

```
git checkout assignment-3
```

###    They can then complete the assignment on that branch, committing their changes with git commit as they go.

##    Once done, they should push that branch up to their fork of the repo on GitHub. They would run:

```
git push origin assignment-3
```

###    Finally, they can go to GitHub and open a new pull request from that branch on their fork into the parent repo.

You would then receive the pull request and can review the changes, merge them in to merge the submission, or just leave the PR open as an "assignment submission".

For the next assignment, students would just need to repeat the fetch, checkout, complete, and push steps to continue working through the assignments in the course.

