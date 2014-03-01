require 'middleman-gh-pages'

task :default => [:build]

desc "Run the preview server at http://localhost:4567"
task :server do
  system("middleman server")
end

# Alias for server
task :s => [:server]