# Dharam's Fork Instructions
This fork incorporates changes to make terraform plan changes more readable, specifically for postmates data eng folks
```
brew uninstall terraform_landscape
cd ~/postmates/ && git clone git@github.com:dharamsk/terraform-landscape.git && cd terraform-landscape
brew install ruby
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
sudo gem install bundler
bundler
gem build terraform_landscape.gemspec
gem install terraform_landscape-0.3.2.gem && rm terraform_landscape-0.3.2.gem
echo "alias landscape='/usr/local/lib/ruby/gems/2.6.0/gems/terraform_landscape-0.3.2/bin/landscape'" >>~/.bash_profile
source ~/.bash_profile
```
(change ~/.bash_profile to .bash_rc or other as necessary)
(if the path is invalid, find the landscape executable and fix the last line above. Might be a diff version of ruby..)
(you can find the path to the executable by running `gem info terraform_landscape`)

# Terraform Landscape

[![Gem Version](https://badge.fury.io/rb/terraform_landscape.svg)](http://badge.fury.io/rb/terraform_landscape)
[![CircleCI](https://circleci.com/gh/coinbase/terraform-landscape.svg?style=svg)](https://circleci.com/gh/coinbase/terraform-landscape)

Terraform Landscape is a tool for reformatting the output of `terraform plan`
to be easier to read and understand.

#### Before
<img src="./doc/before.png" width="65%" alt="Original Terraform plan output" />

### After
<img src="./doc/after.png" width="65%" alt="Improved Terraform plan output" />

* [Requirements](#requirements)
* [Installation](#installation)
* [Usage](#usage)

## Requirements

* Ruby 2.5+

## Installation

The `landscape` executable is installed via [RubyGems](https://rubygems.org/).

```bash
gem install terraform_landscape
```

### macOS

Terraform Landscape is also available via [Homebrew](https://brew.sh/).

```bash
brew install terraform_landscape
```

## Usage

Pipe the output of `terraform plan` into `landscape` to reformat the output.

```bash
terraform plan ... | landscape
```

## Docker

Build the docker image using provided Dockerfile and use it directly:

```bash
docker build . -t landscape
terraform plan ... | docker run -i --rm landscape
```

## License

This project is released under the [Apache 2.0 license](LICENSE).
