desc 'Publish to kyanny.me'
task :publish do
  origin = "https://github.com/kyanny/middleman-kyanny.github.com/commit/#{`git rev-parse head`.chomp}"

  sh 'middleman build'
  sh "rsync -a --delete --exclude=.git build /tmp"
  Dir.chdir('/tmp') do
    sh 'rm -rf kyanny.github.com'
    sh 'git clone git@github.com:kyanny/kyanny.github.com.git'
    Dir.chdir('kyanny.github.com') do
      sh "rsync -a --delete --exclude=.git /tmp/build/ ."
      sh "git add -A"
      sh "git commit -m 'Published: #{origin}'"
      sh "git push -u origin master"
    end
  end
end
