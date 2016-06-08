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
  sh 'chef exec foodcritic -f correctness .'
  sh 'chef exec rubocop'
end

task :syntax do
  # TODO: Verify version has been bumped
end

desc 'Run unit tests with ChefSpec'
task :unit do
  sh 'chef exec rspec --color -fd'
end

desc 'Run functional tests with Serverspec'
task :functional do
  sh 'kitchen test'
end
