# Commands that I ran to even get going...

This helped https://stackoverflow.com/questions/51126403/you-dont-have-write-permissions-for-the-library-ruby-gems-2-3-0-directory-ma

```
brew install rbenv
brew install chruby ruby-install
```

The second command there told me the following:
```
Add the following to the ~/.bash_profile or ~/.zshrc file:
  source /usr/local/opt/chruby/share/chruby/chruby.sh

To enable auto-switching of Rubies specified by .ruby-version files,
add the following to ~/.bash_profile or ~/.zshrc:
  source /usr/local/opt/chruby/share/chruby/auto.sh
```

Which I did. Then I ran this to try to get the latest version of ruby:
```
ruby-install ruby
```


That command failed and I ended up doing this:
https://github.com/rbenv/ruby-build/discussions/2118#discussioncomment-4594287

```
brew install libyaml-devel libyaml
brew update && brew upgrade ruby-build
rbenv install --list
rbenv install 3.2.2
```

This didn't really work though...was still getting some weird errors. So I tried this re https://github.com/rbenv/ruby-build/issues/1409#issuecomment-594478968:
```
xcode-select --install
rbenv install 3.2.2
```

# Ruby 3.2.2 is Installed
Once ruby 3.2.2 was installed (I picked that version cause that's what Mastodon is using re https://github.com/mastodon/mastodon/blob/main/.ruby-version)

I was able to set the local and global ruby versions with `rbenv`:
```
rbenv global 3.2.2
rbenv local 3.2.2
```

And that should have worked, but I needed to add this to my bash_profile:
```
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```

Now with that working, I think we should be good to go....But I was seeing a strange thing `chruby: unknown Ruby: 3.2.2` so I tried:
```
ruby-install ruby-3.2.2
```

# Gems

```
gem install rails
gem update --system 3.4.13
rails --version
```

For some reason though in a new tab this didn't work...so I had to do:
```
gem install rails
gem pristine debug --version 1.7.1
gem pristine rbs --version 2.8.2
```

# Running code

These are the helpful things that I did so far

```bash
# Run the server
$ blog/bin/rails server

# Get a ruby console
$ blog/bin/rails console

# Create a new model
$ blog/bin/rails generate model Article title:string body:text

# Run the migration. I.e. save the model
$ blog/bin/rails db:migrate

# See all the routes
$ blog/bin/rails routes

# Save the controller
$ blog/bin/rails generate controller Comments
```

In a console, you can do things like this:
```ruby
article = Article.new(title: "Hello Rails", body: "I am on Rails!")
article.save  # This will save the article to the DB

# Article is the model Article. article is the object of type Article
Article.find(1)
Article.all
```
