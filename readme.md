#Kaleidoscope Version Control Tidbits

Some fun ways to make version control and Kaleidoscope dance.

Everything is git right now, but glad to take pull requests for other kinds of VCS.

These all assume you've configured Kaleidoscope as your default git difftool. If you use it as a non default tool, you'd change `git difftool` to `git difftool -y -t Kaleidoscope`, but the rest is the same.

##KSReview

KSReview is a useful way to do codereviews of feature branches. It will send all the work done on a feature branch since it diverged from master or a specified mainline branch to Kaleidoscope.

__Git Alias__

`ksreview = "!sh -c 'SHA=${1:-HEAD}; BRANCH=${2:-master}; if [ $SHA == $BRANCH ] ; then SHA=HEAD; fi; BASE_SHA=$(git merge-base $BRANCH $SHA); git difftool $BASE_SHA $SHA;' -"`

__Git One liner__

`git config --global alias.ksreview "\!sh -c 'SHA=\${1:-HEAD}; BRANCH=\${2:-master}; if [ \$SHA == \$BRANCH ] ; then SHA=HEAD; fi; BASE_SHA=\$(git merge-base \$BRANCH \$SHA); git difftool \$BASE_SHA \$SHA;' -"`

__Git Usage__

To review HEAD with master as your mainline branch

`git ksreview`

To review a branch or sha when master is your mainline branch

`git ksreview some-feature-branch-or-sha`

To review a branch (or sha) by name with a custom mainline branch

`git ksreview some-feature-branch-or-sha mainline-branch`

##KSShow

This one comes care of https://twitter.com/stevelosh/status/270931273214746625 with the addition of HEAD as a default value.

KSShow gives you the contents of an arbitrary sha in Kaleidoscope.

__Git Alias__

`ksshow = "!sh -c 'SHA=${1:-HEAD}; git difftool $SHA^..$SHA;' -"`

__Git One liner__

`git config --global alias.ksshow "\!sh -c 'SHA=\${1:-HEAD}; git difftool \$SHA^..\$SHA;' -"`

__Git Usage__

To open the most recent commit on the current branch in Kaleidoscope

`git ksshow`

To open an arbitrary sha in Kaleidoscope

`git ksshow some-sha`
