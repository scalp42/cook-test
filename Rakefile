#!/usr/bin/env rake

# http://acrmp.github.com/foodcritic/
require 'foodcritic'
# https://github.com/turboladen/tailor
require 'tailor/rake_task'

task :default => [:tailor, :foodcritic, :knife, :chefspec]

Tailor::RakeTask.new do |task|
  task.file_set('attributes/**/*.rb', "attributes") do |style|
    style.max_line_length 100, level: :warn
  end
  task.file_set('definitions/**/*.rb', "definitions")
  task.file_set('libraries/**/*.rb', "libraries")
  task.file_set('metadata.rb', "metadata")
  task.file_set('providers/**/*.rb', "providers")
  task.file_set('recipes/**/*.rb', "recipes") do |style|
    style.max_line_length 100, level: :warn
  end
  task.file_set('resources/**/*.rb', "resources")
  # task.file_set('templates/**/*.erb', "templates")
end

FoodCritic::Rake::LintTask.new do |t|
  t.options = { :fail_tags => ['correctness'] }
end

# http://berkshelf.com/
desc "Install Berkshelf to local cookbooks path"
task :berks do
  sh %{berks install --path cookbooks}
end

# http://wiki.opscode.com/display/chef/Managing+Cookbooks+With+Knife#ManagingCookbooksWithKnife-test
desc "Test cookbooks via knife"
task :knife do
  sh %{knife cookbook test -o cookbooks -a}
end

# https://github.com/acrmp/chefspec
desc "Run ChefSpec Unit Tests"
task :chefspec do
  sh %{rspec --color cookbooks/cook-test}
end
