# git 如何 revert 一个已经 merge 的 commit

业务突然暴出来，某个需求还没有开发就发到了线上，在同事的帮助下找到了那个出问题的 Merge Request（后面称为PR）。心想找到了PR就好办了，revert掉就行了，但是有意思的地方来了，revert 啥都没发生。如下:

```bash
▶ git revert 241b5485495e713af0b2e9c3213f09d672e166f2
On branch PT-revert
Your branch is behind 'h/master' by 3 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean
```

看到这个报错，我心里有个猜测：git 不知道我要revert的是哪个commit。

然后就搜了下，果然有网友遇到了同样的问题：[How to revert a merge commit that's already pushed to remote branch?](https://stackoverflow.com/a/7100005/9672709)，验证了我的猜测，git生成的merge节点 出现了分叉，直接revert git可能也不知道咋revert。开一下git的[revert官方文档](https://git-scm.com/docs/git-revert#Documentation/git-revert.txt---mainlineparent-number)有个`-m`参数，并且给出了另一个文档的链接，[How to revert a faulty merge](https://github.com/git/git/blob/master/Documentation/howto/revert-a-faulty-merge.txt)。

还见识到了 rebase 的`--no-ff`操作。突然就想了 merge 的 fast forward 模式的好了。

突然想到一个很应景的一句话：“you don't know what you don't know（你不知道你不知道的）”，第一次听来自极客时间《左耳朵耗子》栏目（[酷壳 coolshell](https://coolshell.cn/)的作者），还好平时 git 稍微熟练一些，不然解决起来会很费时间。
