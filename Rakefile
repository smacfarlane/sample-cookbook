task default: :verify

desc 'Verify cookbook'
task verify: [:lint, :syntax, :unit]

# desc 'Build cookbook'
# task build: [:lint, :syntax, :unit, :security, :quality, :publish]
#
# desc 'Accept cookbook'
# task acceptance: [:provision, :deploy, :smoke, :functional]

desc 'Run linting tools -- foodcritic and rubocop'
task :lint do
  sh 'foodcritic -X spec .'
end

task :syntax do
  sh 'chefstyle'
end

desc 'Run unit tests with ChefSpec'
task :unit do
  sh 'chef exec rspec --color -fd'
end

desc 'Run functional tests with Serverspec'
task :functional do
  sh 'kitchen test'
end
