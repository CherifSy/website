.. _daycamp_04:


Lesson 4: Version Control
=========================

What We'll Cover
----------------

* Nano, a command line editor
* What's Git
* Using ``git``
* What's GitHub
* More resources

Nano
----

* type like normal
* Use arrow keys to move around
* ^ means hold control while pressing the key

.. figure:: /static/nano.png
   :align: center

Why Bother?
-----------

.. figure:: /static/phd_final.gif
 :scale: 75%
 :align: right

Image from
`PhD Comics <http://www.phdcomics.com/comics/archive.php?comicid=1531>`_


..  Version Control is Hard
    -----------------------

..  .. figure:: /static/xkcd_1296.png
       :scale: 150%
       :align: center

..  Image from `XKCD <http://xkcd.com/1296>`_

Better Options: Version Control
-------------------------------

* Commit = Snapshot of part of your project's state
* Centralized (SVN, CVS) vs. Decentralized (Git, hg)
* We'll look at Git today
    * Easier to learn other VCS from Git
    * Widely used in the open source world

Git
---

.. figure:: /static/Linus_Torvalds.jpeg
    :align: left

git, noun. Brit.informal.
1. an unpleasant or contemptible person.

Setting up Git
--------------

* In VM:

.. code-block:: bash

    $ sudo yum install git
    $ git config --global user.name "My Name"
    $ git config --global user.email "myself@gmail.com"
    $ git config --global core.editor "nano"

Using Git Locally
-----------------

.. code-block:: none

    $ git init

.. note:: This initializes a git repo. Use `man git-init` for more info.

.. code-block:: none

    $ git add <filename>

.. note:: This puts <filename> into the staging area. It isn't committed yet.
    Use ``git diff`` to see what changes aren't yet in staging.

.. code-block:: none

    $ git commit -m "I did a thing!"

.. note:: This actually makes the commit. Use ``git status`` to see what's in
    staging but not yet committed. Use ``git show`` or ``git log`` to see
    recent commits.

* Undo things?
  the `git book <http://git-scm.com/book/en/Git-Basics-Undoing-Things>`_ explains
  well

* Did I remember to commit that?

.. code-block:: none

  $ git status

* What commits have I made lately?

.. code-block:: none

    $ git log

What Not To Do
--------------

* Don't delete the .git files

.. note:: If you kill them, git loses its memory :(

* Avoid redundant copies of the same work in one revision
* Don't make "oops, undoing that" commits.
    * Use git commit --amend or git revert

.. note:: Amending is fine as long as you haven't pushed yet. It's generally a
    bad idea to amend or rebase work that you've already shared with others,
    unless you really know what you're doing.

* Don't wait too long between commits
    * You can squash them all together later

.. note:: Commit every time you think you might want to return to the current
    state. You can revert back to any previous commit, but there is no way to
    magically add a commit in where you forgot to make one.

* Don't commit secrets...

.. note:: Yes, there are ways to sort of take them down off of GitHub, but
    somebody might have cloned your repo while it had the secrets in. Once
    someone has a piece of information, you can't just take it away.

.. figure:: /static/dont_do_this.jpg
    :scale: 50%
    :align: right

http://arstechnica.com/security/2013/01/psa-dont-upload-your-important-passwords-to-github/

Git Exercise
------------

First create a git repository!

.. code-block:: none

    $ mkdir my_python_app
    $ cd my_python_app
    $ git init

Git will do a one-time prompt for some basic information and then you have a
Git Repository! All code in this code can be tracked by git as a single
project.

Adding Code
-----------

Create and open a new file ``script.py`` with the following command:

.. code-block:: none

    $ nano script.py

.. code-block:: python

    def f(x):
        print(x**x)
    if __name__ ==  "__main__":
        f(5)

Save this file and leave the text editor and tell git to track this code.

.. code-block:: none

    $ git status
    $ git add script.py
    $ git commit -m "My first git commit!"
    $ git status
    $ git log

Cloning a Repository
--------------------

Git also allows you to ``clone`` a remote repository to work on another
person's code. It's like downloading the entire project and it's git history.

.. code-block:: none

    $ cd ~
    $ git clone <some git url>
    $ cd <new repo directory>
    $ ls

You have successfully clone a remote repository and can start modifying the
other person's code. Changes you make on your local version of this project
will not affect the original version you modified (although you can push
changes if you are allowed to do so by the original owner!)

Cloned Repository Part 2
------------------------

.. code-block:: none

    $ git clone https://github.com/DevOpsBootcamp/tinsy-flask-app.git

See http://git.io/vcVmB for more details.

Let's use our application we just cloned. The README should include
installation instructions

.. code-block:: none

    $ cd tiny-flask-app
    $ virtualenv venv
    $ pip install -r requirements.txt
    $ python script.py

Now if you go to <your ip address>:<http port> you can see a live version of
the app!



Branches
--------

Github allows you to 'branch' your codebase. This allows you to make changes
on a separate track without modifying the original codebse in the same
repository. Branches are preserved when you clone a remote repository.

.. code-block:: none

    $ git checkout broken
    $ python myapp.py

Now you can see your webapp doesn't work correctly when you try to access it in
the browser!

We can manually go in and fix it, or run a command to see what changed between
this version and the version in the 'master' branch.

.. code-block:: none

    $ git diff master

Daily workflow
--------------

.. figure:: /static/gitflow.png
    :scale: 75%
    :align: right

Pull -> Work -> Add changes -> Commit -> Push

Larger projects have more complex workflows

.. note:: The picture is of the Git Flow branching model, and you'll probably
    see it every single time anyone explains Git branching and merging to you.

GitHub!
-------

.. figure:: /static/octocat.jpg

.. note:: GitHub serves a threefold purpose:

    * Makes it easier to manage permissions & share code with others
    * Backs up all your work in case bad things happen to your laptop
    * Social/gamification/resume building

    It also has `amazing documentation <https://help.github.com/>`_ which you
    should all go read right now and consult whenever you're the least bit
    confused. It's like the Ubuntu forums in that it's explained in a way the
    newbies can understand, but unlike them in that it's all written by people
    who know what they're doing.

* Free online code storage
* Easily share and collaborate on code
* Great Git documentation
* Easily findable source-code

Other Resources
---------------

`Git Visualizations <http://www.wei-wang.com/ExplainGitWithD3/#>`_

`Further tiny-flask-app exercises <https://github.com/DevOpsBootcamp/tinsy-flask-app#now-what>`_
