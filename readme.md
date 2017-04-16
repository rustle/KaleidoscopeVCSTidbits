# Kaleidoscope Version Control Tidbits

Some fun ways to make version control and Kaleidoscope dance.

Everything is git right now, but glad to take pull requests for other kinds of VCS.

## KSReview

KSReview is a useful way to do codereviews of feature branches. It will send all the work done on a feature branch since it diverged from master or a specified mainline branch to Kaleidoscope.

__Git Alias__

`ksreview = "!sh -c 'SHA=${1:-HEAD}; BRANCH=${2:-master}; if [ $SHA == $BRANCH ] ; then SHA=HEAD; fi; git difftool -y -t Kaleidoscope $BRANCH...$SHA;' -"`

__Git One Liner__


`git config --global alias.ksreview '!f() { local SHA=${1:-HEAD}; local BRANCH=${2:-master}; if [ $SHA == $BRANCH ]; then SHA=HEAD; fi; git difftool -y -t Kaleidoscope $BRANCH...$SHA; }; f'`

__Git Usage__

To review HEAD with master as your mainline branch

`git ksreview`

To review a branch or sha when master is your mainline branch

`git ksreview some-feature-branch-or-sha`

To review a branch (or sha) by name with a custom mainline branch

`git ksreview some-feature-branch-or-sha mainline-branch`

## KSShow

This one comes care of https://twitter.com/stevelosh/status/270931273214746625 with the addition of HEAD as a default value.

KSShow gives you the contents of an arbitrary sha in Kaleidoscope.

__Git Alias__

`ksshow = "!sh -c 'SHA=${1:-HEAD}; git difftool -y -t Kaleidoscope $SHA^..$SHA;' -"`

__Git One Liner__

`git config --global alias.ksshow '!f() { local SHA=${1:-HEAD}; git difftool -y -t Kaleidoscope $SHA^..$SHA; }; f'`

__Git Usage__

To open the most recent commit on the current branch in Kaleidoscope

`git ksshow`

To open an arbitrary sha in Kaleidoscope

`git ksshow some-sha`

## KSDiff

KSDiff is just a more compact version of `difftool -y -t Kaleidoscope` for people who don't use Kaleidoscope as the default difftool.

__Git Alias__

`ksdiff = difftool -y -t Kaleidoscope`

__Git One Liner__

`git config --global alias.ksdiff "difftool -y -t Kaleidoscope"`

__Git Usage__

To see the contents of the most recent commit

`git ksdiff HEAD^..HEAD`

## Notes

A coworker of mine pointed out that it might be nice to give some of these more idiomatic git like names, so for people that like that kind of thing:

ksreview becomes

`review = "!sh -c 'SHA=${1:-HEAD}; BRANCH=${2:-develop}; if [ $SHA == $BRANCH ] ; then SHA=HEAD; fi; git diff $BRANCH...$SHA;' -"`

and

`reviewtool = "!sh -c 'SHA=${1:-HEAD}; BRANCH=${2:-develop}; if [ $SHA == $BRANCH ] ; then SHA=HEAD; fi; git difftool -y -t Kaleidoscope $BRANCH...$SHA;' -"`

ksshow becomes

`showtool = "!sh -c 'SHA=${1:-HEAD}; git difftool -y -t Kaleidoscope $SHA^..$SHA;' -"`