# Welcome to the HyP3-paper contributing guide
Thank you for taking the time to look at this work. This repository contains the manuscript that describes HyP3 and will be submitted to the Journal of Open Source Science. If you are not an author on the paper (e.g., are not or have never been on the HyP3 team) please refrain from making pull requests to this repository. Instead, please create an issue describing the changes you would like to see. After you submit your issue, a member of our team will review it.

For HyP3 team members, please read the information below:

## Contributing Guide

### Workflow
We are striving to make the writing of this manuscript as similar to a GitOps software project as possible. For this reason, please follow a general [forking workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow) when making contributions. Please make you PRs as small as possible so that we can promote quick iterations.

The basic steps are:
1. Fork the repository
2. Clone your fork
   ```
   git clone https://github.com/[OWNER]/hyp3.git
   ```
3. Add this repository as an `upstream` remote
   ```
   git remote add upstream https://github.com/ASFHyP3/hyp3-paper.git
   ```  
4. Create a feature branch based on the upstream/develop branch
   ```
   git fetch --all --prune
   git checkout --no-track -b [NAME] upstream/develop
   ```
5. Make your changes! Then push them to your fork
   ```
   git push -u origin [NAME]
   ```
6. Propose your changes by opening a pull request to `ASFHyP3/hyp3-paper`'s `develop` branch

### Guidelines
Guidelines are less solidified for Markdown projects, but pleases adhere to these rules:

1. Use US English spellings
2. Paragraphs should be soft-wrapped, with no maximum line length
3. Refer to the [JOSS submission guidelines](https://joss.readthedocs.io/en/latest/submitting.html) when creating sections headers and layout

### GitHub Actions
We have implemented several GitHub Actions that are run when PRs are created, or new commits are pushed to an existing PR. These include checks for spelling and valid links, as well as an action that builds a JOSS formatted PDF of `paper/paper.md` if any of these actions fail, please take the actions necessary to ensure they pass.

In some cases, domain-specific words are flagged by the spell check action as misspelled since they are not in the spell check's dictionary. If this happens, please add the relevant words to the dictionary file (IN ALPHABETICAL ORDER) located at `.github/dictionary.txt`. This should remove the issue for these words.

