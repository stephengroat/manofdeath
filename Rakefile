# frozen_string_literal: true

require 'pry'
require 'rugged'
require 'rubocop/rake_task'
require 'tmpdir'

task default: %w[doc rubocop]

task :doc do
  Dir.mktmpdir('terraform') do |dir|
    repo = Rugged::Repository.clone_at('https://github.com/hashicorp/terraform',
                                       dir)
    repo.tags.each do |tag|
      next unless tag.name =~ /^v\d*\.\d*\.\d*$/

      begin
        puts tag.canonical_name
        repo.checkout(tag.canonical_name)
      rescue StandardError => e
        puts e.message
      end
    end
  end
end

RuboCop::RakeTask.new
