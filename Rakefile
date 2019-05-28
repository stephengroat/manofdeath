# frozen_string_literal: true

require 'pry'
require 'git'
require 'rubocop/rake_task'
require 'tmpdir'

task default: %w[doc rubocop]

task :doc do
  Dir.mktmpdir('terraform') do |dir|
    repo = Git.clone('https://github.com/hashicorp/terraform',
                     'terraform',
                     path: dir)
    repo.tags.each do |tag|
      next unless tag.name =~ /^v\d*\.\d*\.\d*$/

      puts tag.name
      repo.checkout(tag.name)
    end
  end
end

RuboCop::RakeTask.new
