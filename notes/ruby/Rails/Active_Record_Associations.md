
# [Active Record Associations](https://guides.rubyonrails.org/association_basics.html)


Rails supports six types of associations, each with a particular use-case in mind.

Here is a list of all of the supported types with a link to their API docs for more detailed information on how to use them, their method parameters, etc.

* belongs_to
* has_one
* has_many
* has_many :through
* has_one :through
* has_and_belongs_to_many



The simplest rule of thumb is that you should set up a has_many :through relationship if you need to work with the relationship model as an independent entity. If you don't need to do anything with the relationship model, it may be simpler to set up a has_and_belongs_to_many relationship (though you'll need to remember to create the joining table in the database).

You should use has_many :through if you need validations, callbacks, or extra attributes on the join model.
While has_and_belongs_to_many suggests creating a join table with no primary key via id: false, consider using a composite primary key for the join table in the has_many :through relationship. For example, it's recommended to use create_table :manifests, primary_key: [:assembly_id, :part_id] in the example above.

2.9 Polymorphic Associations
A slightly more advanced twist on associations is the polymorphic association. With polymorphic associations, a model can belong to more than one other model, on a single association. For example, you might have a picture model that belongs to either an employee model or a product model. Here's how this could be declared:

```
class Picture < ApplicationRecord
  belongs_to :imageable, polymorphic: true
end

class Employee < ApplicationRecord
  has_many :pictures, as: :imageable
end

class Product < ApplicationRecord
  has_many :pictures, as: :imageable
end
```

from
3 Tips, Tricks, and Warnings