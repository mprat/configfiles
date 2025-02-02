require 'rake/clean'

CLEAN.include FileList['bash_profile', 'screenrc', 'tmux.conf', 'gitconfig', 'vimrc', 'zshrc'].pathmap("#{ENV['HOME']}/.%p")

desc "Set up Linux environment"
task :setup_linux => [:apt, :common, :zim_ubuntu, :python, :apt_long] do
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
  sh "sudo apt-get -y install build-essential libffi-dev libbz2-dev liblzma-dev"
  sh "sudo apt-get -y install git git-core vim tmux zsh tig curl git-lfs"
  sh "sudo apt-get -y install ruby ruby-dev rubygems"
  sh "sudo apt-get -y install python3-pip python3-software-properties"
  sh "sudo apt-get -y install sqlite3 libsqlite3-dev"
  sh "sudo apt-get -y install libssl-dev libcurl4-openssl-dev"
  sh "sudo apt-get -y install zlib1g-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev"
  # for all the printer driverz
  sh "sudo apt-get -y install printer-driver-gutenprint"
end

desc "Setup node"
task :setup_node do
  # sh "sudo apt-get -y install nodejs npm"
  sh "curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash"
end

desc "Install more packages that take a long time"
task :apt_long do
  sh "sudo apt-get -y install xclip mesa-utils"
  sh "sudo apt-get -y install inkscape"
  sh "sudo apt-get -y install texlive-full"
end

desc "Screen recorder on Linux"
task :linux_screen_recorder do
	sh "sudo add-apt-repository ppa:maarten-baert/simplescreenrecorder"
	sh "sudo apt-get update"
	sh "sudo apt-get install simplescreenrecorder"
end

desc "Install SQL on Linux"
task :linux_sql do
  sh "sudo apt-get install mysql-server"
  sh "sudo apt-get install libmysqlclient-dev"
  # sh "sudo mysql_secure_installation"
  sh "sudo mysql_install_db"
end

desc "Install zim wiki on Ubuntu"
task :zim_ubuntu do
  sh "sudo apt-add-repository ppa:jaap.karssenberg/zim"
  sh "sudo apt-get update"
  sh "sudo apt-get install zim"
end

desc "Set up python development env"
task :python do
   # this is to enable compiling python with pyenv with tk support
  sh "sudo apt-get -y install tk-dev"
  sh "curl https://pyenv.run | bash"
end

desc "Install Zotero"
task :zotero_linux do
  sh "wget -qO- https://raw.githubusercontent.com/retorquere/zotero-deb/master/install.sh | sudo bash"
  sh "sudo apt update && sudo apt -y install zotero"
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
