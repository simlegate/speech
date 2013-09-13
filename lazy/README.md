* 将命名的作用域包在 lambda 里来惰性地初始化。 

```ruby
# 差劲
class User < ActiveRecord::Base
  scope :active, where(active: true)
  scope :inactive, where(active: false)

  scope :with_orders, joins(:orders).select('distinct(users.id)')
end

# 好
class User < ActiveRecord::Base
  scope :active, -> { where(active: true) }
  scope :inactive, -> { where(active: false) }

  scope :with_orders, -> { joins(:orders).select('distinct(users.id)') }
end

```
