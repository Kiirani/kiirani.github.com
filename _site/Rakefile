task :default => :debug

task :clean do
	sh 'rm -rf _site'
end

task :build => :clean do 
	sh 'jekyll build'
	puts "Site built."
end

task :debug do
	sh 'jekyll serve --watch'
end


task :publish do 
	bold = %x[tput bold]
	normal = %x[tput sgr0]
	puts "\n\n#{bold}Enter a commit message:#{normal} "
	message = STDIN.gets
	commit = %x[echo '#{message}' | git commit-tree dev^{tree}:_site -p $(cat .git/refs/heads/master)] 
	%x[git update-ref refs/heads/master #{commit}]
	puts "Commited build to master; ready to push"
end
