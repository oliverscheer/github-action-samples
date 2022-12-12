# GitHub Actions Samples

My samples about GitHub Actions that I learned in multiple customer projects.

You can find the official documentation on GitHub Actions here: <https://docs.github.com/en/actions/learn-github-actions>

## Introduction

I'm a big fan of GitHub Actions because they are easy to develop and helps very much in automation almost everything.

## My Tipps & Tricks

### 1. Generate better outputs in logs

Some bash scripts can generate a lot of valuable output, or a loooooong list to scroll down to find the right information. During some projects I learnt some helpful tricks, that I want to share here with you.

```yaml
steps:
      - shell: bash
        run: |
          echo "# Results" >> $GITHUB_STEP_SUMMARY

          echo "::group::My very long list"
          echo "Log output of execution"
          for i in {1..100}
          do
            echo "Log $i"
          done
          echo "::endgroup::"

          echo "::group::My title 2"
          echo "Inside group"
          echo "Inside group"
          echo "::add-mask::Mona The Octocat"
          echo "Inside group"
          echo "::endgroup::"
```

The output will look like:
![img](media/improved_logging.png)

If required you can expanded the list:
![img](media/improved_logging_expanded.png)


### 2. Add outputs to the summary page

I was reading the logs of each step to check if something was successful or for some outputs during some tasks.

Then I just learned that you can generate some extra entries for the summary page of your workflow.

```yaml
jobs:
  prepare-job:
    runs-on: ubuntu-latest
    name: Prepare
    steps:
        # Writing into step summary
        echo "New resource group created with name ABC" >> $GITHUB_STEP_SUMMARY

        echo ":rocket: Preparation successful" >> $GITHUB_STEP_SUMMARY
        echo "| Key | Value |" >> $GITHUB_STEP_SUMMARY
        echo "| --- | ----- |" >> $GITHUB_STEP_SUMMARY
        echo "| A   | 'red' |" >> $GITHUB_STEP_SUMMARY
        echo "| B   | 42    |" >> $GITHUB_STEP_SUMMARY
        echo "| C   | 3.141 |" >> $GITHUB_STEP_SUMMARY
```

This will result to this output on the summary page, as soon as the step is done.

![img](media/step_summary.png)

### 3. Use artifacts for outputs and inputs

Not new, but extrem helpful in finding issues, or get access to remote generated content. Just create some files, and upload them as artifacts. You can download them easily in other jobs in the same workflow. This makes sense if you build something on linux for example, but need it on windows in a later step, for example.

```yaml
steps:

  - id: generate-log-file
    shell: bash
    run: |
        for i in {1..100}
        do
        echo "Log $i" > log.txt
        done

  - id: upload-log-file
    use:  uses: actions/upload-artifact@v3
    with:
        name: log.txt
        path: log.txt
```

![img](media/artifacts.png)

### 4. Trigger manually on demand and use inputs

GitHub Actions are very dynamic and can be configured by input variables that you can use inside the logic.

You can define to run the workflow manually on GitHub with the `workflow_dispatch` trigger:

```yaml
name: Output Demo
on:
  workflow_dispatch:
    inputs:
      username:
        description: "The name of the user"
        default: "Oliver"
        required: true
```


![img](media/inputs.png)

In later steps you can access those inputs very simple with the followin snippet:

```yaml
echo "Hello ${{ inputs.username }}"
```

## Summary

After applying some of my favorite tricks the summary page looks like this:

![img](media/full_summary.png)


Coming next:
- Test workflows in a branch
- Build Re-usable components
- Good practices for naming inputs and environment vars
- Parallel execution
- Write an az cli like action
- Context
- add linting but only for added/changed files
