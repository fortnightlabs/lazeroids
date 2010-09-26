load 'deploy' if respond_to?(:namespace) # cap2 differentiator
Dir['vendor/plugins/*/recipes/*.rb'].each { |plugin| load(plugin) }

default_run_options[:pty] = true

set :application, "lazeroids"
set :repository,  "git://github.com/fortnightlabs/lazeroids.git"
set :scm, :git

set :user, "app"

role :app, "lazeroids"
set :use_sudo, false

namespace :deploy do
  task :start, :roles => :app do
    run "#{try_sudo} start lazeroids"
  end

  task :stop, :roles => :app do
    run "#{try_sudo} stop lazeroids"
  end

  task :restart, :roles => :app, :except => { :no_release => true } do
    run "#{try_sudo} restart lazeroids"
  end
end

namespace :npm do
  task :install, :roles => :app do
    run "cd #{release_path} && /u/apps/.nodelocal/bin/npm install ."
  end
end
after "deploy:update_code", "npm:install"