require 'rake'
require 'github_api'

task :trigger_build, [:repos] do |t, args|
  repos = Github::Repos.new :oauth_token => ENV['GITHUB_API_KEY']

  args[:repos].split(' ').each do |repo|
    owner, repo_name = repo.split('/')
    hooks = repos.hooks.list owner, repo_name
    shippable_hook = hooks.select { |h| h.config.url and h.config.url.include? 'shippable.com' }.first
    if shippable_hook
      repos.hooks.test owner, repo_name, shippable_hook.id
      puts "Triggered Shippable build for project #{repo}"
    else
      puts "Project #{repo} does not seem to be configured with Shippable"
    end
  end
end

task :default
