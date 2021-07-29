# Using OpsChain and MintPress together

This document covers the relationship between OpsChain and MintPress.

## MintPress overview

[MintPress](https://www.limepoint.com/mintpress) is a LimePoint automation tool with a strong foundation in the Oracle ecosphere.

## Using the MintPress SDK from OpsChain

OpsChain bundles the MintPress SDK for use by customers with an existing MintPress licence.

All the MintPress controller gems included in the MintPress SDK are available in the OpsChain runner and can be used by adding them to your project Gemfile and then requiring them in your `actions.rb`.

### Example: using the `Mint::Secret` class in OpsChain

MintPress provides the [`Mint::Secret` class](https://docs.limepoint.com/reference/ruby/Mint/Secret.html) to hide secret values from accidental leakage into server logs.

The `Mint::Secret` class is provided by the MintPress `mintpress-common` gem, to access it in your OpsChain action, add that gem to your Gemfile:

```ruby
# any existing gems
gem 'mintpress-common'
```

Once the gem has been added, `mintpress-common` can be required and an instance of the `Mint::Secret` can be created. Below is a simple `actions.rb` which uses the MintPress `Mint::Secret` class:

```ruby
require 'opschain'
require 'mintpress-common'

action :default do
  password = Mint::Secret.new('password')
  puts password
end
```

Running this example with OpsChain (for example using the `opschain-action` command) will print the obfuscated output rather than the secret value:

```bash
$ opschain-action default
********
```

## Licence & authors

- Author:: LimePoint (support@limepoint.com)

See [LICENCE](../../LICENCE)