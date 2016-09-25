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
  sh "sudo apt-get -y install build-essential"
  sh "sudo apt-get -y install git git-core vim tmux zsh tig curl"
  sh "sudo apt-get -y install ruby ruby-dev rubygems"
  sh "sudo apt-get -y install python-pip python-software-properties"
  sh "sudo apt-get -y install sqlite3 libsqlite3-dev"
  sh "sudo apt-get -y install nodejs npm nodejs-legacy"
  sh "sudo apt-get -y install libssl-dev libcurl4-openssl-dev"
  sh "sudo apt-get -y install zlib1g-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev"
  sh "sudo apt-get -y install xclip libffi-dev mesa-utils"
  sh "sudo apt-get -y install inkscape"
end

desc "Install zim wiki on Ubuntu"
task :zim_ubuntu do
  sh "sudo apt-add-repository ppa:jaap.karssenberg/zim"
  sh "sudo apt-get update"
  sh "sudo apt-get install zim"
end

desc "Set up python development env"
task :python do
  sh "pip install --upgrade pip"
	sh "pip install virtualenv"
	sh "pip install virtualenvwrapper"
  sh "source /usr/local/bin/virtualenvwrapper.sh"
  sh "mkvirtualenv science"
  sh "pip install -r science_requirements.txt"
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
