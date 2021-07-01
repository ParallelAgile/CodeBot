# CodeBot documentation

(page under heavy heavy construction...)

CodeBot is a low-code, full-stack, domain-driven application generator. You can set up a trial account and take it for a spin here:  https://parallelagile.net

If you're using CodeBot on your project and would like to help improve or add to this documentation, please feel free to clone the project and post a Pull Request here...

Feedback is also welcome!  (Email us at support@parallelagile.com).

## Contributing

### First time setup

* Fork the CodeBot repo to your account by clicking [Fork](https://github.com/ParallelAgile/CodeBot/fork) button

* Clone the CodeBot repository locally.

    ```
    $ git clone https://github.com/ParallelAgile/CodeBot
    $ cd CodeBot
    ```

* Run the following commands to setup your fork as a remote to push your work to. Replace {USERNAME} with your own
github username. The default remote for the ParallelAgile is "origin'

    ```
    $ git remote add fork https://github.com/{USERNAME}/CodeBot
    ```

* Install [jekyll requirements](https://jekyllrb.com/docs/installation/#guides) based on your OS.


### Running Locally

* Install all of the required gems from your specified sources (make sure you are in the CodeBot folder
before running):

    ```
    $ bundle install
    ```

* Start the server to host the doc locally:

    ```
    $ bundle exec jekyll serve
    ```

### Pull Requests

* Create a branch for the issue you want to work on:

    ```
    $ git fetch origin
    $ git checkout -b your-branch-name origin/master
    ```

* Make changes and [commit as you go](https://dont-be-afraid-to-commit.readthedocs.io/en/latest/git/commandlinegit.html#commit-your-changes).

    ```
    $ git add {filename}
    $ git commit -m "{COMMIT MESSAGE}"
    ```

* Push your commits to your fork on GitHub and create a pull request.

    ```
    $ git push --set-upstream fork your-branch-name
    ```