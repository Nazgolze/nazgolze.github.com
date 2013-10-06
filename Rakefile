require '~/.gem/ruby/2.0.0/gems/jekyll-1.2.1/lib/jekyll.rb'
require 'tmpdir'

GITHUB_REPONAME = "Nazgolze/nazgolze.github.com"

desc "Generate blog files"
task :generate do
Jekyll::Site.new(Jekyll.configuration({
  "source"      => ".",
  "destination" => "_site"
  })).process
end


desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp
    Dir.chdir tmp
    system "git init"
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.shellescape}"
    system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
    system "git push origin master --force"
  end
end

