# Rebase example


```
while true
do
	git log --graph --pretty=oneline --abbrev-commit --decorate --all
	sleep .2
	clear
done
```

```
mkdir app
cd app
git init

echo foo > somefile
git add -A
git commit -m 'Foo'

echo foo again >> somefile
git commit -am 'Foo again'

git checkout HEAD~1
git checkout -b catdog
echo bar > another
git add -A
git commit -m 'Bar'

echo baz >> another
git commit -am 'Baz'
```

```
git rebase -i master
git checkout master
git merge catdog
git branch -d catdog
```

```
git log --graph --pretty=oneline --abbrev-commit --decorate --all
* 9bac4d4 (HEAD -> catdog) Baz
* 52e4d8b Bar
| * 17a04a1 (master) Foo again
|/
* 610e893 Foo
git rebase -i master
[detached HEAD 1bb0650] Foo yet again
 Date: Thu Apr 19 17:23:40 2018 -0700
 1 file changed, 2 insertions(+)
 create mode 100644 another
Successfully rebased and updated refs/heads/catdog.
git log --graph --pretty=oneline --abbrev-commit --decorate --all
* 1bb0650 (HEAD -> catdog) Foo yet again
* 17a04a1 (master) Foo again
* 610e893 Foo
git checkout master
Switched to branch 'master'
git log --graph --pretty=oneline --abbrev-commit --decorate --all
* 1bb0650 (catdog) Foo yet again
* 17a04a1 (HEAD -> master) Foo again
* 610e893 Foo
git merge catdog
Updating 17a04a1..1bb0650
Fast-forward
 another | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 another
git log --graph --pretty=oneline --abbrev-commit --decorate --all
* 1bb0650 (HEAD -> master, catdog) Foo yet again
* 17a04a1 Foo again
* 610e893 Foo
git branch -d catdog
Deleted branch catdog (was 1bb0650).
git log --graph --pretty=oneline --abbrev-commit --decorate --all
* 1bb0650 (HEAD -> master) Foo yet again
* 17a04a1 Foo again
* 610e893 Foo
```