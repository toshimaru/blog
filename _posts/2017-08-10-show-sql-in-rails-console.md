---
layout: post
title: Show SQL queries in rails console
tags: rails activerecord
last_modified_at: 2019-12-24
---

When you set `log_level` `:info` (mostly on production server), the SQL outputs are disabled in `rails console`.

```rb
# Rails Configuration
Rails.application.configure do
  ...
  config.log_level = :info
  ...
end
```

```ruby
# $ rails c
> Model.count
=> 12345
# No Query is shown
```

If you want to see SQL generated by `Model.count`, What you need is setting log level manually.

> The available log levels are: :debug, :info, :warn, :error, :fatal, and :unknown, corresponding to the log level numbers from 0 up to 5, respectively. To change the default log level
>
> ```rb
> config.log_level = :warn # In any environment > initializer, or
> Rails.logger.level = 0 # at any time
> ```

via. [Log Levels - Debugging Rails Applications — Ruby on Rails Guides](http://guides.rubyonrails.org/debugging_rails_applications.html#log-levels)

```rb
# $ rails c
> Rails.logger.level = 0
=> :debug

> Model.count
   (1.8ms)  SELECT COUNT(*) FROM `models`
=> 12345
```

Now, you can check the queries in `rails console`.
