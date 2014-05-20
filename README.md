= ActsAsDuration

Say you have an attribute in your ActiveRecord model called `total_minutes`. Simply add `acts_as_duration :total_minutes` and you'll automatically get the following getter/setter methods:

```ruby
total_seconds
total_seconds=
total_hours
total_hours=
total_days
total_days=
total_hhmmss
total_hhmmss=
```

Note: the getter methods will always return a Float (except hhmmss, which returns a string). The setter methods will accept an Integer, String, or Float.

Note: the base attribute name should contain either 'seconds', 'minutes', 'hours', 'days', or 'hhmmss' otherwise the gem can't know the base unit. Alternatively, you can specify the unit like this `acts_as_duration :total_consumed, attr_unit: :minutes`

```ruby
class Foo < ActiveRecord::Base
  attr_accessor :total_minutes
  acts_as_duration :total_minutes  
end

foo = Foo.new(total_minutes: 400)
song.total_minutes
# 400
song.total_seconds
# 24000.0
song.total_seconds = 1500
# 1500
song.total_minutes
# 25.0

## You also have a hhmmss method which converts a string to time

song.total_hhmmss = "24:12:34"
# "24:12:34"
song.total_days
# 1.01
song.total_hours
# 24.21
song.total_hhmmss = "48"
# "48"
song.total_days
# 2.0
```

## Arguments

You can call it on multiple attributes at once and include options at the end.
`acts_as_duration :total_minutes, :completed_days, read_only: true`

options:
 `attr_unit:`
 		description: Specify the unit of the base attribute (not necessary if it's part of the attribute name like e.g. 'total_seconds')
		valid values: Either :seconds, :minutes, :hours, :days, or :hhmmss
 `read_only:`
 		description: If true, will only create the getter method and not the setter
 		valid_values: true or false
 


This project rocks and uses MIT-LICENSE.