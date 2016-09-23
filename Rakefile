require 'rake/clean'

CLEAN.include FileList['bash_profile'].pathmap("#{ENV['HOME']}/.%p")

desc "Set up Linux environment"
task :setup_linux => [:apt] do
  puts "Setting up Linux dotfiles."

  link_file("bash_profile_linux", ".bash_profile")
end

desc "Set up OSX environment"
task :setup_osx do
  puts "Setting up OSX dotfiles."

  link_file("bash_profile_osx", ".bash_profile")
end

desc "Install packages from apt"
task :apt do
  sh "sudo apt-get update"
  sh "sudo apt-get -y install git vim tmux zsh"
end

def link_file(script, dotname=nil)
	if dotname == nil
		dotname = ".#{script}"
	end
	dotfile = File.join(ENV['HOME'], dotname)
	if File.exist? dotfile
		warn "~/#{dotname} already exists"
	else
		ln_s File.join(File.dirname(__FILE__), script), dotfile
	end
end
