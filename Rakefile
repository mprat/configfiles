require 'rake/clean'

CLEAN.include FileList['bash_profile', 'screenrc', 'tmux.conf', 'gitconfig', 'vimrc', 'zshrc'].pathmap("#{ENV['HOME']}/.%p")

desc "Set up Linux environment"
task :setup_linux => [:apt, :common] do
  puts "Setting up Linux dotfiles."

  link_file("bash_profile_linux", ".bash_profile")
end

desc "Set up OSX environment"
task :setup_osx => [:common] do
  puts "Setting up OSX dotfiles."

  link_file("bash_profile_osx", ".bash_profile")
end

desc "Common tasks"
task :common do
  %w[screenrc tmux.conf gitconfig vimrc zshrc].each do |script|
  		link_file(script)
  end
end

desc "Install packages from apt"
task :apt do
  sh "sudo apt-get update"
  sh "sudo apt-get -y install git vim tmux zsh tig xclip rubygemsi git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev python-pip"
end

desc "Set up python development env"
task :python do
  sh "pip install --upgrade pip"
	sh "pip install virtualenv"
	sh "pip install virtualenvwrapper"
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
