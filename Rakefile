task default: :accept

desc 'Run all acceptance tests'
task accept: [:lint, :unit]

desc 'Run linting tools -- foodcritic and rubocop'
task :lint do
  sh 'foodcritic -X spec .'
  sh 'rubocop'
end

desc 'Run unit tests with ChefSpec'
task :unit do
  sh 'chef exec rspec --color -fd'
end

desc 'Run functional tests with Serverspec'
task :functional do
  sh 'kitchen test'
end
