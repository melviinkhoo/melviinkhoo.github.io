# set environment variable BUNDLER_ENABLE_RPM_PREFERRING to 'true' to enable bundler patch
# if enabled bundler prefers rpm-gems even if they are older version then gems in gem-repo
if ENV['BUNDLER_ENABLE_RPM_PREFERRING'] == 'true'
  require File.join(File.dirname(__FILE__), 'lib', 'bundler_patch_rpm-gems_preferred')
end

# load Katello configuration
path = File.expand_path('../lib', __FILE__)
$LOAD_PATH << path unless $LOAD_PATH.include? path
require 'katello_config'

# When adding new version requirement check out EPEL6 repository first
# and use this version if possible. Also check Fedora version (usually higher).
# With a pull request, send also link to our (or Fedora) koji with RPMs.
source 'http://rubygems.org'

gem 'jemoji'
gem 'rails', '3.0.10'
gem 'json'
gem 'rest-client', :require => 'rest_client'
gem 'jammit', '>= 0.5.4'
gem 'rails_warden', '>= 0.5.2'
gem 'net-ldap'
gem 'oauth'
gem 'ldap_fluff'

if defined? JRUBY_VERSION
  gem 'jruby-openssl'
  gem 'activerecord-jdbcpostgresql-adapter', '1.1.3'
  gem 'tire', '>= 0.3.0'
else
  gem 'thin', '>= 1.2.8'
  gem 'tire', '>= 0.3.0', '< 0.4'
  gem 'pg'
end

gem 'delayed_job', '~> 2.1.4'
gem 'daemons', '>= 1.1.4'
gem 'uuidtools'

# Stuff for view/display/frontend
group :assets do
  gem 'haml', '>= 3.1.2'
  gem 'haml-rails', "= 0.3.4"
  gem 'compass', '>= 0.11.5'
  if `uname -a` =~ /f16/
    gem 'compass', '0.11.5'
  else
    gem 'compass', '0.12.2'
    gem 'compass-rails', '~> 1.0.3'
  end
  gem 'compass-960-plugin', '>= 0.10.4', :require => 'ninesixty'
  gem 'simple-navigation', '>= 3.3.4'
end

# Stuff for i18n
gem 'gettext_i18n_rails'
gem 'i18n_data', '>= 0.2.6', :require => 'i18n_data'

# Reports - TODO this is hack that needs to be removed once ruport is officially released
if system('rpm -q rubygem-ruport >/dev/null')
  gem 'ruport', '>=1.7.0'
else
  gem 'ruport', '>=1.7.0', :git => 'git://github.com/ruport/ruport.git'
end
#not an actual katello dependency, but 
#Does not pull in  hashery, matches RPM
gem 'pdf-reader', '<= 1.1.1'

gem 'prawn'
gem 'acts_as_reportable', '>=1.1.1', :require => 'ruport/acts_as_reportable'

# Documentation
gem "apipie-rails", '>= 0.0.13'

# Load all sub-gemfiles from bundler.d directory
Dir[File.expand_path('bundler.d/*.rb', File.dirname(__FILE__))].each do |bundle|
  self.instance_eval(Bundler.read_file(bundle), bundle)
end
