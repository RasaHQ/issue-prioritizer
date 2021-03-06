# Issue Prioritizer

Prioritizes issues in a specified column of a GitHub project board.


## Usage

You can use it as follows in your GitHub workflow:

```yml
jobs:
  prioritize_project_issues:
    runs-on: ubuntu-latest
    name: Automatically reorder issues by priority in "Backlog" column.
    steps:
      - uses: RasaHQ/issue-prioritizer@master
        with:
          token: ${{ secrets.CUSTOM_GITHUB_TOKEN }}  # you need a GitHub token with enough permissions
          column_id: 42
          order: priority:critical,priority:high,priority:normal,priority:low
          default_label: priority:normal
```

It will reorder cards in your project, including notes that are not yet converted to issues. If some issues are unlabelled, you can define a `default_label` to consider for these: it will make the action behave as if the issue was correctly labelled, but doesn't assign the label. It works for notes too.

You will need to grant the `admin:org` (to list and move project cards) and `repo` (to access to issues labels) scopes to your GitHub token.


## Develop

After checking out a copy of the repository locally, you run `yarn` or `npm install .` to install dependencies.

To run the script, you will need to pass environment variables that correspond to the inputs of the action:
```bash
INPUT_COLUMN_ID=42 INPUT_TOKEN=xxx INPUT_ORDER="priority:critical,priority:high,priority:normal,priority:low" INPUT_DEFAULT_LABEL="priority:normal" node index.js
```

That's it 🚀

## Build

Use `zeit/ncc` to build `issue-prioritizer`

1. Install `zeit/ncc` by running this command in your terminal: `npm i -g @zeit/ncc`
2. Compile your `index.js` file using the following command: `ncc build index.js`

As a result, a file `dist/index.js` with your code and the compiled modules will be generated.
You should always commit this file because GitHub uses it to run the action.
