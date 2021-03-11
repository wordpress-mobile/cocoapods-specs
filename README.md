# CocoaPods Specs Repository for Automattic

This repository contains the `.podspec` files for pods that are used internally by Automattic, to develop our iOS and macOS apps.

## How to use

To use any of the Pods published in this internal spec repository, you will need to add this repository as a `source` at the top of your `Podfile`.

Note that since you will likely want to still also use public pods (published by the CocoaPods community on trunk / the CDN) in addition to Automattic's pods, you will need to add CocoaPods's CDN as a source explicitly too.

```ruby
source 'https://github.com/wordpress-mobile/cocoapods-specs.git'
source 'https://cdn.cocoapods.org/'
```
 
_CocoaPods implicitly uses the CDN as a source if there is no explicit `source` declaration at all in your `Podfile`; but as soon as you add at least one source, you need to explicitly declare all the sources you want to use, including the CDN._

## Source order and Security Considerations

For security reasons, when adding the `source` declarations to your `Podfile`, you should add Automattic's spec repo first, and the CDN last.

This is because when CocoaPods looks up pods, it searches the various `sources` _in the order they are declared_. That means that if someone publishes a malicious pod in the CDN but with the same name as one of Automattic's pod, and you declared the CDN earlier in your `source` declarations, that malicious pod would take precedence over the one from Automattic. While declaring Automattic's spec repo first and the CDN later will give Automattic's source precedence and avoid any name spoofing attack.
