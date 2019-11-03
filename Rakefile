##### General configuration #####
require 'ostruct'
SITE = OpenStruct.new
SITE.output_dir = File.expand_path(File.join(File.dirname(__FILE__), *%w[build]))
SITE.rsync_args = %w[-av]
SITE.user       = 'geeksam'
SITE.host       = 'think-like-a-git.net'
SITE.remote_dir = '/home/geeksam/think-like-a-git.net/'


##### Site building #####
desc 'Build the site'
task :build do
  sh 'middleman build'
end

task :clear_build_dir do
  sh "rm -rf #{SITE.output_dir}"
end

desc 'Completely rebuild the site'
task :rebuild => ['clear_build_dir', 'build']


##### Deployment #####
#require 'rake/contrib/sshpublisher'
namespace :deploy do
  desc 'Deploy to the server using rsync'
  task :rsync do
    cmd = "rsync #{SITE.rsync_args.join(' ')} "
    cmd << "#{SITE.output_dir}/ #{SITE.user}@#{SITE.host}:#{SITE.remote_dir}"
    sh cmd
  end
end

namespace :deploy do
  task :github do
    sh "rm -rf docs"
    sh "mv build docs"
  end
end

desc 'deploy the site to the webserver'
task :deploy => ['rebuild', 'deploy:github']
