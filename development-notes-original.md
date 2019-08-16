Notes below are specifically made for all macOS X Catalina users, but also suitably apply to macOS X mojave users and loosely apply to CentOS/RedHat 6.4+ users. Should it be desired later on, updates can be made to list specific commands for every platform

Installation of System Requirements

There are three schools of thought here: brew-full, brew-less, and crazy

Brew-less

Installation without Homebrew, also what’s most likely to be compatible with other systems, either macOS X pre-Mojave (10.14) or other UNIX based platforms

On macOS X, you should either run with MacPorts or Joyent’s pkgin, which I recommend for most systems outside of the pkgsrc platform(s).

Install the 64-bit libraries and verify the SHA1 checksums:

run: BOOTSTRAP_TAR="bootstrap-trunk-x86_64-20190524.tar.gz"

run: BOOTSTRAP_SHA="1c554a806fb41dcc382ef33e64841ace13988479"

run: curl -O https://pkgsrc.joyent.com/packages/Darwin/bootstrap/${BOOTSTRAP_TAR}

run: echo "${BOOTSTRAP_SHA}  ${BOOTSTRAP_TAR}" >check-shasum

run: shasum -c check-shasum

run: sudo tar -zxpf ${BOOTSTRAP_TAR} -C /

run: eval $(/usr/libexec/path_helper)

Add-in some helpful aliases to make the continual process easier:

run: echo "alias refresh=”source ~/.zshrc” >> ~/.zshrc" 

(assumption here is zsh, but if you have bash, then do ~/.bash_profile)

run: echo "alias edT="nano ~/.zshrc" >> ~/.zshrc"

run: echo "alias alias ..='cd ..' alias ...='cd ../../' alias ....='cd ../../../' alias .....='cd ../../../../' alias ......='cd ../../../../../' >> ~/.zshrc"

run: echo "alias editPW='SUDO_EDITOR=open -FWne sudo -e' >> ~/.zshrc"

run: echo "alias alias pkg-sec-check='sudo pkg_admin fetch-pkg-vulnerabilities'"

run: echo "alias pkg-orphans='sudo pkgin -y autoremove'"

Run update, upgrade and then autoremove for dependency fixes

run: pkg update

run: pkg -y full-upgrade

run: pkg -y autoremove

Optional search for vulnerable packages, etc:

run: mkdir /Users/<username>/etc

run: sudo touch /etc/daily.conf && /etc/security.conf

run: sudo echo “fetch_pkg_vulnerabilities=YES” >> ~/etc/daily.conf

run: sudo echo “check_pkg_vulnerabilities=YES” >> ~/etc/security.conf

Extra packages installs for necessary tools with this process (unless you’re on Catalina, you don’t likely need all of these, you can always remove the extras, or could prevent installing too many)

pkg in rc.subr-20181226 pkgsrc-todo-1.3nb3 pkgsrc-guide-tools-1.0nb1 pkgse-0.3nb7 pkgfind-20111022 pkgdiff-1.8nb3 pkgclean-20051116 pkg_select-20090308nb8 pkg_regress-0.4 pkg_online-server-0.13.1 pkg_online-client-0.13.1nb1 nih-0.14.1 lintpkgsrc-4.94nb1 genpkgng-20140425 distbb-0.47.2 rsync-3.1.3nb1 sysbuild-2.7nb2 py27-pip py27-pypiserver pv pipestatus pipebench netpipes pgbouncer-1.9.0 pgbuildfarm-4.15.1nb2 postgresql_autodoc-1.30nb7 slony1-2.2.7 wbm-postgresql-1.831 py37-psycopg2-2.8.3 py37-barman-2.5 postgresql96-server-9.6.14 postgresql96-redislog-0.2 postgresql96-pltcl-9.6.14 postgresql96-plpython-9.6.14 postgresql96-plperl-9.6.14 postgresql96-docs-9.6.14 postgresql96-contrib-9.6.14 postgresql96-client-9.6.14 postgresql96-9.6.14 postgres_exporter-0.4.7 phppgadmin-5.1nb1 php73-pgsql-7.3.8 php73-pdo_pgsql-7.3.8 php73-davical-1.1.8 p5-postgresql-1.9.0nb21osm2pgsql-0.96.0nb3 odbc-postgresql-9.0.200nb5 lua53-sql-postgres-2.3.2nb1 libpqxx-6.2.2nb1 libdbi-driver-pgsql-0.9.0nb1 libgda-postgres-5.2.9 freeradius-pgsql-3.0.19 erlang-p1_pgsql-1.1.6 collectd-postgresql96-5.8.0nb1 clisp-pgsql-2.49nb2

Note: Please do not install p5-pip as it conflicts with the python version of the same tool, and will ruin you’re native OS installation 

Secondary Note: If you miss or otherwise enjoy using UNIX based tools/environments, all of those tools can be found under pkgsrc/pkgin with the heirloom-* tag, where all of them are run this way:

pkg in heirloom-yes-070715 heirloom-xargs-070715 heirloom-whodo-070715 heirloom-whoami-070715 heirloom-what-070715 heirloom-wc-070715 heirloom-units-070715 heirloom-uniq-070715 heirloom-uname-070715 heirloom-ul-070715nb1 heirloom-tty-070715 heirloom-tsort-070715 heirloom-tr-070715 heirloom-touch-070715 heirloom-time-070715 heirloom-tee-070715 heirloom-tail-070715 heirloom-sync-070715 heirloom-sum-070715   heirloom-stty-070715 heirloom-split-070715 heirloom-sort-070715 heirloom-sleep-070715 heirloom-setpgrp-070715 heirloom-sdiff-070715 heirloom-rmdir-070715 heirloom-renice-070715 heirloom-random-070715 heirloom-pwd-070715 heirloom-printf-070715 heirloom-printenv-070715 heirloom-pr-070715 heirloom-pg-070715nb1 heirloom-pathchk-070715 heirloom-paste-070715 heirloom-od-070715 heirloom-nohup-070715 heirloom-nl-070715 heirloom-nice-070715 heirloom-news-070715 heirloom-more-070715nb1 heirloom-mkfifo-070715 heirloom-mkdir-070715 heirloom-mesg-070715 heirloom-mailx-12.5nb1 heirloom-ls-070715nb1 heirloom-logname-070715 heirloom-logins-070715 heirloom-ln-070715 heirloom-listusers-070715 heirloom-line-070715 heirloom-libcommon-070715nb1 heirloom-join-070715 heirloom-id-070715 heirloom-hostname-070715 heirloom-head-070715 heirloom-hd-070715 heirloom-groups-070715 heirloom-grep-070715 heirloom-getopt-070715 heirloom-getconf-070715 heirloom-fold-070715 heirloom-fmt-070715 heirloom-file-070715 heirloom-factor-070715 heirloom-env-070715 heirloom-doctools-160308 heirloom-doc-070715 heirloom-dirname-070715 heirloom-diff3-070715 heirloom-cut-070715 heirloom-csplit-070715 heirloom-cp-070715 heirloom-copy-070715 heirloom-comm-070715 heirloom-col-070715 heirloom-cmp-070715 heirloom-cksum-070715 heirloom-chown-070715 heirloom-chmod-07071 heirloom-cat-070715 heirloom-calendar-070715 heirloom-cal-070715 heirloom-bfs-070715 heirloom-bdiff-070715 heirloom-basename-070715 heirloom-banner-070715 heirloom-awk-070715

PKGIN via Joyent Source/Information Page

Some of the packages required Nodejs so you can always hit run: pkg in nodejs npm

Global installation of Gem dependencies: 

sudo gem install pristine json xcpretty rspec draper ahoy paperclip active-admin webpacker webpack wrapper cowl clearwater sys-filesystem actionna absolutely 2do 99design-tasks pry activerecord-import fastlane figaro rdoc jruby bcrypt bundler primary rollout wicked_pdf cocoon nested_form grape rake geocoder vcr parallel_tests capistrano bundler-audit shoulda-matchers devise_masquerade sidekiq-cron ancestry paranoia aasm papertrail globalize database_cleaner factory_girl simplecov rails_best_practices binding_of_caller pry-byebug letter_opener rolify puma unicorn-rails capistrano redis sucker_punch pgsearch dotenv administrate metatags money-rails

Note: If you don’t install these gems at the system level, you won’t be able to use them in individual, local, shell or even system based alternative environments with different Ruby versions.

Heroku Installation: 

Has to be done through the installation client, not through brew, regardless of which version you go

login: heroku login 

clone getting started: git clone https://github.com/heroku/python-getting-started.git

deploying getting started app: heroku create && git push heroku master && heroku ps:scale web=1 && heroku open

reviewing test logs: heroku logs --tails

installing local dependencies: pip install -r requirements.txt 

ironically requires dependencies

postgres

python (try to base it on your system version or python 2.7, whichever is oldest)

pip

PAUSE HEROKU

RBENV Installation:

create a repository in your root user folder, to save your sanity

cd /into/the/userfolder/path 

run: git clone git clone https://github.com/rbenv/rbenv.git ~/.rbenv

compiling a dynamic bash extension to speed rbenv up: cd ~/.rbenv && src/configure && make -C src

run: echo ‘export PATH=$HOME/.rbenv/bin:$PATH”’ >> ~/.zshrc

run: echo ‘eval “$(rbenv init -)”’ >> ~/.zshrc OR can also run: ~/.rbenv/bin/rbenv init

hooking rbenv into your shell:  

run the rbenv-doctor script in order to make sure everything is working properly

curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash
Checking for `rbenv' in PATH: /usr/local/bin/rbenv
Checking for rbenv shims in PATH: OK
Checking `rbenv install' support: /usr/local/bin/rbenv-install (ruby-build 20170523)
Counting installed Ruby versions: none
  There aren't any Ruby versions installed under `~/.rbenv/versions'.
  You can install Ruby versions like so: rbenv install 2.2.4
Checking RubyGems settings: OK
Auditing installed plugins: OK

PLEASE NOTE: In most instances, know that this doesn’t work, so you might want to go ahead and follow the ruby-build path instead of the regular rbenv install process built into rbenv

run: source ~/.zshrc

test your installation with a little test:

run: rbenv install 2.4.2

run: rbenv local 2.4.2 into a specific project folder

run: rbenv rehash and then you can always check ruby --version  

You can always use something like the rbenv-installer and the following link:  

ruby-build:

In order to install these versions of ruby and your OS (of any kind) to use it, you need at least one of two packages: ruby-build or ruby-install, but you would do better to be with at least ruby-build, because it has a ruby-install as part of it

You have two options: as a plugin or as a standalone application… If you were doing this in brew.sh it would essentially operate the same way as the plugin, so I would recommend that method over the latter:

plugin route

run: mkdir -p "$(rbenv root)"/plugins

run: git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build

standalone application/program

run: git clone https://github.com/rbenv/ruby-build.git

run: PREFIX=/usr/local ./ruby-build/install.sh

upgrading or updating

cd "$(rbenv root)"/plugins/ruby-build && git pull with the plugin

as a general git pull with the repository

more information about the use of ruby-build and applying patches with:  

Install Needed Ruby Gems:

gem install bundler

gem env home just to double check the installer

gem install rbenv

you can choose to run ruby without a version or choose to dump the shell version with: rbenv shell --unset

INSTALL POSTGRES: I would HIGHLY recommend using something like: https://postgresapp.com

RETURNING TO HEROKU 

navigate to your folder with the Heroku project

run: cat Gemfile to read and make sure you know the required ruby version

run: rbenv install <version>

run: rbenv local <version>

run: gem install bundler rake rake_db rake_heroku pristine executable-hooks rake_dashboard capistrano

run: bundle

optional run: bundle exec rake db:setup, where you add the bundle exec because more often than not, the rake version on your system is more updated than the repo/project

CELEBRATE WITH A HAPPY DANCE… and maybe a taco!  

Brew-full

Installation with Homebrew, without reliance on other package management solutions. The only reason this method would be recommended against, is if you are doing so on your naked system. If you are performing these scripts/installations within a containerized environment, this makes the most amount of sense for ease of use/logging/adjustment/development.

Homebrew packages manager

run: /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

run: echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc

run: brew doctor to make sure your environment is set properly

run: brew update

run: brew upgrade

run: brew install curl wget bower rbenv ruby-build tree pkg-config node icu4c auto-conf openssl npm ncurses pcap postgres yarn zlib heroku-toolbelt

run: curl https://bootstrap.pypa.io/get-pip.py > get-pip.py && sudo python get-pip.py

run: pip --version to make sure it worked  

PLEASE NOTE: You may see a message about errors regarding certificates within

Crazy

WIP…

