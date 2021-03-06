# encoding: utf-8

require 'rubygems'
require 'bundler'
begin
  Bundler.setup(:default, :development)
rescue Bundler::BundlerError => e
  $stderr.puts e.message
  $stderr.puts "Run `bundle install` to install missing gems"
  exit e.status_code
end
require 'rake'

require 'jeweler'
Jeweler::Tasks.new do |gem|
  # gem is a Gem::Specification... see http://docs.rubygems.org/read/chapter/20 for more options
  gem.name = "bio-faster"
  gem.homepage = "http://github.com/fstrozzi/bioruby-faster"
  gem.license = "MIT"
  gem.summary = %Q{A fast parser for Fasta and FastQ files}
  gem.description = %Q{A fast parser for Fasta and FastQ files}
  gem.email = "francesco.strozzi@gmail.com"
  gem.authors = ["Francesco Strozzi"]
  gem.required_ruby_version = '>= 1.9'
  # dependencies defined in Gemfile
end
Jeweler::RubygemsDotOrgTasks.new

require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/test_*.rb'
  test.verbose = true
end

require 'rcov/rcovtask'
Rcov::RcovTask.new do |test|
  test.libs << 'test'
  test.pattern = 'test/**/test_*.rb'
  test.verbose = true
  test.rcov_opts << '--exclude "gems/*"'
end

desc "Run all specs"
task :spec do
  FileList['spec/**/*_spec.rb'].each do |spec|
    sh "rspec #{spec}"
  end
end

task :default => :test

require 'rake/rdoctask'
Rake::RDocTask.new do |rdoc|
  version = File.exist?('VERSION') ? File.read('VERSION') : ""

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "bio-faster #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

namespace :ext do
  desc "Compile extension"
  task :build do
    puts "Building extension"
    cd File.join(File.dirname(__FILE__),"ext")
    sh "ruby "+File.join(File.dirname(__FILE__),"ext","extconf.rb")
    sh "make"
    FileList["*.log"].each do |file|
      rm file
    end
    FileList["*.o"].each do |file|
      rm file
    end
      
  end
end

