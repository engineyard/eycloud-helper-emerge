# Emerge helpers for EY Cloud

This cookbook holds 2 definitions, one called enable_package and one called update_file.  Between these two definitions it enables you to 'unmask' a package in Chef and then install an 'masked' version of said package.

## Usage

For example if you want to install Libxml 2.7.6 on AppCloud you would use the following as a recipe.

```ruby
enable_package "dev-libs/libxml2" do
  version "2.7.6"
end

package "dev-libs/libxml2" do
  version "2.7.6"
  action :install
end
```

There is also the following which will update `/etc/portage/package.unmask/local`

```ruby
enable_package "x11-libs/#{package}" do
  version node[:qt_webkit_version]
  unmask true
end
```

Alternately, this example shows you how to modify the 'use_flags' that are used during package compilation too.

```ruby
enable_package "dev-lang/ruby" do
  version "1.8.7_p299"
end

package_use "dev-lang/ruby" do
  flags "threads"
end

package "dev-lang/ruby" do
  version "1.8.7_p299"
  action :install
end
```

## Terminology

Gentoo uses the names 'mask' and 'unmask' terminology between stable and unstable.  Typically this is done in /etc/make.conf with ACCEPT_KEYWORDS declaration for '~amd64' and '~x86'.  However it can also be added to /etc/portage/package.keywords/local to 'unmask' packages individually.

## Installation

INSTALLATION HERE

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License

MIT LICENSE