# Installing rubocop pre-commit hook!

> Navigate to project directory (more formally navigate to location where your .git is.)


+ Intall rubocop:
    - Add `gem 'rubocop', '~> 1.16', require: false` to your Gemfile.
    - Run `bundle install` while in `devsnest` directory.

> #### Navigate back to `backend` directory.

+ Add pre-commit hook:
    - Create new file `pre-commit` in `.git/hooks` directory. Simply put, you can use `vi ./.git/hooks/pre-commit`.
    - Copy this in the `pre-commit` file

    ```shell
  set -e

    cd "${0%/*}/../.."

    echo "Running rubocop on your changes"


    # for modified files
    if [[ $(git diff --name-only) ]]; then
        git diff --diff-filter=AM --name-only | xargs rubocop
    fi

    # for staged files
    if [[ $(git diff --name-only --cached) ]]; then
        git diff --diff-filter=AM --name-only --cached | xargs rubocop
    fi
    
    ```

    - Run `chmod +x ./.git/hooks/pre-commit` to make it executable.




#### Now rubocop will run with every commit for your changes.

> Note : to bypass rubocup checks use `-n` or `--no-verify` with `git commit`.


