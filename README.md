## About me

[My CV](https://pccofvns.github.io)

## Setup

- Setup [Jekyll](https://jekyllrb.com/docs/installation/)

```shell
brew install chruby ruby-install xz
ruby-install ruby
# If you’re using Bash, replace .zshrc with .bash_profile
echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
 # run 'chruby' to see actual version
echo "chruby ruby-3.3.4" >> ~/.zshrc
source ~/.zshrc
rm Gemfile
bundle install jekyll
bundle exec jekyll serve
```

## References

1. [Jekyll Installation](https://jekyllrb.com/docs/installation/)
