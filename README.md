# finsync-inspire

## Internal Repos:

### FINSYNC Registration
* review the requirements listed in the `Gemfile` via run: `cat Gemfile` within the repository
* declare the ruby version, with `rbenv` like run: `rbenv local #.#.#`
* install required/dependency gems via run: `gem install bundle bundler pristine rack rackdb rack-heroku rspec executable-hooks foreman`
* for good measure as a double-check try to review via run: `bundle exec rspec`
* assuming there isn't anything missing you can move on, OR if there are, run: `bundle install`
* copy over the example environment to the environment variables file expected with run: `cp example.env .env`
* after running redis with `redis-server`, then go ahead and run the creation of a new database `bundle exec rake db:create`
* to avoid migration errors run: `bin/rails db:migrate RAILS_ENV=development`
* to load in your local browser run: `bundle exec foreman start web` _(make sure if you run multiples, you'll have to pass `-p ####` as in, port #### so you can have the port different)_