# dotfiles
I like to have the same configurations on two machines that I use.  To make
things as simple and easy to manage as possible, I maintain this `dotfiles`
repo here in github, with a clone of said repo on each machine; I pull changes
periodically on each machine to refresh to the latest versions.

## How I proceed
Let’s assume that this repos exists only on github and has not been cloned on
any of my machines yet.

On both machines I would do this:

```
cd
mkdir code
cd code
git clone https://github.com/bengudro/dotfiles
```

On both machines I now have a clone of my dotfiles repo at `~/code/dotfiles`

Also, on both machines, I *remove* the relevant dotfiles and replace them with
*symlinks* to my local git repo.

For example let’s say I want to use the same `~/.vimrc` everywhere; on both
machines I would simply:

```
cd
rm .vimrc
ln -s code/dotfiles/.vimrc .vimrc
```

Now in the future if I make changes to the `~/.vimrc` on either one of my
machines, I simply have to:

```
cd code/dotfiles
git add .vimrc
git commit -m 'Update .vimrc'
git push
```

And next time I am at my other machine, in order to fetch the latest copy of my
`.vimrc`, all I would have to to is:

```
cd code/dotfiles
git pull
```

This works thanks to symlinks.  My `~/.vimrc` does not actually exist anymore
in its expected location, because I deleted it and replaced with a *symlink* to
my local repo.  This avoids having to copy files over every time I `git pull`.

Don’t know if my procedure makes sense, or if it is super safe, but it works!
:)

Also, in order for this to work I need the same ssh key on both machines, for
obvious reasons.
