---
layout: post
title: "updating my capistrano deployment process for rails 4"
date: 2014-12-27 15:14:37 +0100
comments: true
categories: capistrano rails4 ruby deployment
---

Now that I'm getting at the point that I can update the different rails apps regularly,
it's about time to update my deployment process.  
After every deploy I have to :

  * Login to the host
  * Navigate to app/current directory
  * Run bundle
  * Run rake assets:precompile
  * Restart application server

Fuck this!  Let's update.

  * Add capistrano gems to Gemfile

    {% highlight ruby %}
    group :development do
      gem 'capistrano','3.2.1'
      gem 'capistrano-rvm', github: 'capistrano/rvm'
      gem 'capistrano-rails'
      gem 'capistrano-bundler'
    end
    {% endhighlight %}

  * Require specific files in Capfile

    {% highlight ruby %}
    # Load DSL and Setup Up Stages
    require 'capistrano/setup'

    # Includes default deployment tasks
    require 'capistrano/rvm'
    require 'capistrano/deploy'
    require 'capistrano/rails'
    require 'capistrano/rails/migrations'

    # Loads custom tasks from `lib/capistrano/tasks' if you have any defined.
    Dir.glob('lib/capistrano/tasks/*.rake').each { |r| import r }
    {% endhighlight %}

  * Update deploy.rb

    {% highlight ruby %}
    # config valid only for Capistrano 3.1
    lock '3.2.1'

    set :application, 'shops'
    set :repo_url, 'git@dev.suwappu.net:suwappu/shops.git'

    set :deploy_to, '/nfs/apps/shops_production'

    set :ssh_options, {
      forward_agent: true
    }

    set :pty, true
    set :linked_dirs, %w{bin log tmp/pids tmp/cache tmp/sockets vendor/bundle
      public/system}

    # Default value for default_env is {}
    # set :default_env, { path: "/opt/rbenv/shims:$PATH" }

    set :rvm_type, :user                     # Defaults to: :auto
    set :rvm_ruby_version, 'rbx-2.2.10'      # Defaults to: 'default'
    set :rvm_custom_path, '/usr/local/rvm'  # only needed if not detected

    stage = "production"
    shared_path = "/nfs/apps/shops_production/shared"
    puma_sock    = "unix://#{shared_path}/sockets/puma.sock"
    puma_control = "unix://#{shared_path}/sockets/pumactl.sock"
    puma_state   = "#{shared_path}/sockets/puma.state"
    puma_log     = "#{shared_path}/log/puma-#{stage}.log"

    namespace :deploy do
      desc 'Restart application'
      task :restart do
        on roles(:app), in: :sequence, wait: 5 do
          # Your restart mechanism here, for example:
          # execute :touch, release_path.join('tmp/restart.txt')
          execute 'sudo /etc/init.d/puma restart'
        end
      end

      desc 'Resetting DB & seeding'
      task :db_reset_and_seed do
        on roles(:app) do
          within "#{current_path}" do
            with rails_env: :production do
              execute :rake, "db:migrate:reset"
              execute :rake, "db:seed"
            end
          end
        end
      end

      after :publishing, :restart

      after :restart, :clear_cache do
        on roles(:web), in: :groups, limit: 3, wait: 10 do
        end
      end
    end
    {% endhighlight %}






