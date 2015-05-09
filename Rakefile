require 'rubygems'
require 'rake'
require 'rake/clean'
require 'rake/testtask'
require 'rdoc/task'
require 'rake/packagetask'
require 'rubygems/package_task'

$:.unshift(File.dirname(__FILE__) + "/lib")
require 'treemap'

CLEAN.include FileList['test/*.html', 'test/*.png', 'test/*.svg']
CLEAN.include 'docs'

PKG_NAME      = 'ruby-treemap'
PKG_VERSION   = Treemap::VERSION

desc 'list available tasks'
task :default do
    puts "Run 'rake --tasks' for the list of available tasks"
end

Rake::RDocTask.new do |rdoc|
    rdoc.rdoc_dir = 'docs'
    rdoc.title    = "RubyTreemap"
    rdoc.options << "--all"
    rdoc.options << "-S"
    rdoc.options << "-N"
    rdoc.options << "--main=README"
    rdoc.rdoc_files.include("README", "EXAMPLES", "TODO", "ChangeLog", "lib/*.rb", "lib/**/*.rb")
end

desc "Run unit tests"
Rake::TestTask.new do |t|
    t.libs << "test"
    begin
        require 'rmagick'
        t.pattern = 'test/tc_*.rb'
    rescue LoadError
        t.test_files = ['tc_color.rb','tc_html.rb']
    end
    t.verbose = true
end

spec = Gem::Specification.new do |s|
    s.platform = Gem::Platform::RUBY

    s.name = PKG_NAME
    s.summary = "Treemap visualization in ruby"
    s.description = %q{Treemap visualization in ruby}
    s.version = PKG_VERSION
    s.author = "Andrew Bruno"
    s.email = "aeb@qnot.org"
    s.homepage = "https://github.com/aebruno/ruby-treemap"

    s.has_rdoc = true
    s.extra_rdoc_files = [ "README", "EXAMPLES" ]
    s.rdoc_options = [ "--main", "README" ]
    s.requirements << 'none'

    s.require_path = 'lib'
    s.autorequire = 'treemap'

    s.files = [ "Rakefile", "TODO", "EXAMPLES", "README", "ChangeLog", "COPYING"]
    s.files = s.files + Dir.glob( "lib/**/*" ).delete_if { |item| item.include?( "\.svn" ) }
    s.files = s.files + Dir.glob( "test/**/*" ).delete_if { |item| item.include?( "\.svn" ) }
end

Gem::PackageTask.new(spec) do |p|
    p.need_tar = true
end
