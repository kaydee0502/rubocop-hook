# Installing rubocop pre-commit hook!

> Navigate to project directory (more formally navigate to location where your .git is.)


+ Intall rubocop:
    - Add `gem 'rubocop', require: false` to your Gemfile.
    - Run `bundle install` while in `project` directory.

+ Add pre-commit hook:
    - Create new file `pre-commit` in `.git/hooks` directory. Simply put, you can use `vi ./.git/hooks/pre-commit`.
    - Paste this script in the `pre-commit` file

    ```shell
  #!/usr/bin/env bash

    set -e
    
    cd "${0%/*}/../.."

    echo "Running rubocop on your changes"


    # for modified files
    if [[ $(git diff --name-only) ]]; then
        git diff --diff-filter=AM --name-only | xargs rubocop -A
    fi

    # for staged files
    if [[ $(git diff --name-only --cached) ]]; then
        git diff --diff-filter=AM --name-only --cached | xargs rubocop -A
    fi
    
    ```

    - Run `chmod +x ./.git/hooks/pre-commit` to make it executable.




#### Now rubocop will run with every commit for your changes.

> Note : to bypass rubocup checks use `-n` or `--no-verify` with `git commit`.


