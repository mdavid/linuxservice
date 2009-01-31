require 'rubygems' 
require 'rake'
require 'rake/testtask'
require 'rake/rdoctask'
require 'rake/clean'
require 'rake/contrib/sshpublisher'
require 'ftools'

PKG_VERSION = "0.1"

Gem::manage_gems 
require 'rake/gempackagetask'

spec = Gem::Specification.new do |s| 
    s.name = "opensim-linux-service" 
    s.version = PKG_VERSION 
    s.homepage = "http://forge.opensimulator.org/gf/projects/linuxserver"
    s.platform = Gem::Platform::RUBY 
    s.summary = "Linux service scripts for running OpenSim"
    # s.description = "Implements the iCalendar specification (RFC-2445) in Ruby.  This allows for the generation and parsing of .ics files, which are used by a variety of calendaring applications."
    
    # s.files = FileList["{test,lib,docs,examples}/**/*"].to_a
    s.files = FileList["{init.d}/*"].to_a
    s.files += ["config", "Rakefile", "README", "AUTHORS", "LICENSE", "INSTALL"]
    s.has_rdoc = true 
    s.extra_rdoc_files = ["README", "LICENSE", "AUTHORS", "INSTALL"]
    s.rdoc_options.concat ['--main', 'README']
    
    s.author = "Sean Dague" 
    s.email = "sdague@gmail.com"
end 


Rake::GemPackageTask.new(spec) do |pkg| 
    #pkg.gem_spec = spec
    #pkg.need_gem = false
    pkg.need_tar = true
end

desc "Install init scripts"
task :install do |args|
    File.copy("init.d/opensim","/etc/init.d/opensim", true)
    File.copy("init.d/opensim-grid","/etc/init.d/opensim-grid", true)
    if not File.exists?("/etc/default/opensim")
        File.copy("config","/etc/default/opensim",true)
    end
    
    # This will only work on ubuntu/debian need rules for others
    if File.exists?("/usr/sbin/update-rc.d")
        system("/usr/sbin/update-rc.d opensim defaults ")
        system("/usr/sbin/update-rc.d opensim-grid defaults ")
    end
        
end

desc "Remove init scripts"
task :uninstall do |args|
    File.delete("/etc/init.d/opensim")
    File.delete("/etc/init.d/opensim-grid")
    File.delete("/etc/default/opensim")

    # This will only work on ubuntu/debian need rules for others
    if File.exists?("/usr/sbin/update-rc.d")
        system("/usr/sbin/update-rc.d opensim remove ")
        system("/usr/sbin/update-rc.d opensim-grid remove ")
    end
end
