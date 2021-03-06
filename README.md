# BlackList: dead simple content filtering

This library is just a simple implementation of a blacklist to filter content.
It comes with a set of default words for filtering in `config/black_list.yml`
that were obtained from [noswearing.com](http://www.noswearing.com). You can
add or remove from the list as necessary. It supports two types of filters
currently – exact matches and greedy matches. Exact matches will only match if
the word is found on its own. Greedy matches will find words nested within
other words. It will also work out of the box as a Ruby on Rails plugin. Just
drop it in `vendor/plugins` and it'll work.

Usage is as follows:

```ruby
BlackList.block?("Stupid ass simple.")    => true
BlackList.block?("Squeaky clean.")        => false
BlackList.block?("Assassins!")            => false
```

You can also just search for particular sorts of matches:

```ruby
BlackList.greedy?("Stupid ass simple.")   => false
BlackList.exact?("Stupid ass simple.")    => true
```

It also supports highlighting flagged words:

```ruby
BlackList.highlight("Stupid ass simple.") => "<code><p>Stupid <strong>ass</strong> simple.</p></code>"
BlackList.highlight("Squeaky clean.")     => "<code><p>Squeaky clean.</p></code>"
```
