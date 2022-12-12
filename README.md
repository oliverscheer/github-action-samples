# GitHub Actions Samples

My samples about GitHub Actions that I learned in multiple customer projects.

You can find the official documentation on GitHub Actions here: <https://docs.github.com/en/actions/learn-github-actions>

## Introduction

I'm a big fan of GitHub Actions because they are easy to develop and helps very much in automation almost everything.

## My Tipps & Tricks

### x. Generate better outputs in logs



### x. Add outputs to the summary page

I was reading the logs of each step to check if something was successful or for some outputs during some tasks.

Then I just learned that you can generate some extra entries for the summary page of your workflow.

```bash
# Writing into step summary
echo "New resource group created with name ABC" >> $GITHUB_STEP_SUMMARY

echo ":rocket: Preparation successful" >> $GITHUB_STEP_SUMMARY
echo "| Key | Value |" >> $GITHUB_STEP_SUMMARY
echo "| --- | ----- |" >> $GITHUB_STEP_SUMMARY
echo "| A   | 'red' |" >> $GITHUB_STEP_SUMMARY
echo "| B   | 42    |" >> $GITHUB_STEP_SUMMARY
echo "| C   | 3.141 |" >> $GITHUB_STEP_SUMMARY

```

### x. Use artifacts for outputs and inputs

What was build? And why I didn't run like on my machine?

### x. Test workflows in a branch

### x. Build Re-usable components

### x. Good practices for naming inputs and environment vars

### x. Parallel execution

### x. Write an az cli like action

### x. Context

### x. add linting but only for added/changed files

## Summary
