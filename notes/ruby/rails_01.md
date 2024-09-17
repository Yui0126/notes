# Rails Guide

## [Active Record](https://guides.rubyonrails.org/active_record_basics.html#what-is-active-record-questionmark)

The Active Record pattern is described by Martin Fowler in the book Patterns of Enterprise Application Architecture as "an object that wraps a row in a database table, encapsulates the database access, and adds domain logic to that data." 
**Active Record objects carry both data and behavior.** Active Record classes match very closely to the record structure of the underlying database. This way users can easily read from and write to the database, as you will see in the examples below.


### Object Relational Mapping
Object Relational Mapping, commonly referred to as ORM, is a technique that connects the rich objects of a programming language to tables in a relational database management system (RDBMS). In the case of a Rails application, these are Ruby objects. Using an ORM, the attributes of Ruby objects, as well as the relationship between objects, can be easily stored and retrieved from a database without writing SQL statements directly. Overall, ORMs minimize the amount of database access code you have to write.


## [Convention over Configuration](https://guides.rubyonrails.org/active_record_basics.html#convention-over-configuration-in-active-record)
When writing applications using other programming languages or frameworks, it may be necessary to write a lot of configuration code. This is particularly true for ORM frameworks in general. However, if you follow the conventions adopted by Rails, you'll write very little to no configuration code when creating Active Record models.

Rails adopts the idea that if you configure your applications in the same way most of the time, then that way should be the default. Explicit configuration should be needed only in those cases where you can't follow the convention.


## [Creating Active Record](https://guides.rubyonrails.org/active_record_basics.html#creating-active-record-models)
```
bin/rails generate migration CreateBooks title:string author:string
```
or,

```
bin/rails generate model Book title:string
author:string
```
### Creating Namespaced Models
Active Record models are placed under the app/models directory by default. But you may want to organize your models by placing similar models under their own folder and namespace. For example, order.rb and review.rb under app/models/book with Book::Order and Book::Review class names, respectively. You can create namespaced models with Active Record.

In the case where the Book module does not already exist, the generate command will create everything like this:
```
bin/rails generate model Book::Order
```

If the Book module already exists, you will be asked to resolve the conflict:
```
bin/rails generate model Book::Order
      invoke  active_record
      create    db/migrate/20240305140356_create_book_orders.rb
      create    app/models/book/order.rb
    conflict    app/models/book.rb
  Overwrite /Users/bhumi/Code/rails_guides/app/models/book.rb? (enter "h" for help) [Ynaqdhm]
```

## [Overriding the Naming Conventions](https://guides.rubyonrails.org/active_record_basics.html#overriding-the-naming-conventions)

It's possible to override the column that should be used as the table's primary key using the ActiveRecord::Base.primary_key= method:

```
class Book < ApplicationRecord
  self.primary_key = "book_id"
end
```

## [CRUD](https://guides.rubyonrails.org/active_record_basics.html#crud-reading-and-writing-data)

If a block is provided, both create and new will yield the new object to that block for initialization, while only create will persist the resulting object to the database:

```
book = Book.new do |b|
  b.title = "Metaprogramming Ruby 2"
  b.author = "Paolo Perrotta"
end

book.save
```
We can find specific books with find_by and where. While find_by returns a single record, where returns a list of records:

```
# Returns the first book with a given title or `nil` if no book is found.
book = Book.find_by(title: "Metaprogramming Ruby 2")

# Alternative to Book.find_by(id: 42). Will throw an exception if no matching book is found.
book = Book.find(42)
```

```
# Find all books with a given an author, sort by created_at in reverse chronological order.
Book.where(author: "Douglas Adams").order(created_at: :desc)
```

**There are many more Active Record methods to read and query records. You can learn more about them in the [Active Record Query](https://guides.rubyonrails.org/active_record_querying.html) guide.**

### Update
```
book = Book.find_by(title: "The Lord of the Rings")
book.title = "The Lord of the Rings: The Fellowship of the Ring"
book.save
```
A shorthand for this is,
```
book = Book.find_by(title: "The Lord of the Rings")
book.update(title: "The Lord of the Rings: The Fellowship of the Ring")
```
If you'd like to update several records in bulk without callbacks or validations, you can update the database directly using update_all:
```
Book.update_all(status: "already own")
```

### Delete
If you'd like to delete several records in bulk, you may use destroy_by or destroy_all method:
```
# Find and delete all books by Douglas Adams.
Book.destroy_by(author: "Douglas Adams")

# Delete all books.
Book.destroy_all
```

## [Validations](https://guides.rubyonrails.org/active_record_basics.html#validations)
Methods like save, create and update validate a model before persisting it to the database. When a model is invalid these methods return false and no database operations are performed. All of these methods have a bang counterpart (that is, save!, create! and update!), which are stricter in that they raise an ActiveRecord::RecordInvalid exception when validation fails. A quick example to illustrate:

You can learn more about validations in the [Active Record Validations](https://guides.rubyonrails.org/active_record_validations.html) guide.


## [Callbacks](https://guides.rubyonrails.org/active_record_basics.html#callbacks)
Callbacks allow you to trigger logic before or after a change to an object's state. They are methods that get called at certain moments of an object's life cycle. With callbacks it is possible to write code that will run whenever an Active Record object is initialized, created, saved, updated, deleted, validated, or loaded from the database.
Learn more about [Active Record Callbacks](https://guides.rubyonrails.org/active_record_callbacks.html).

## [Migrations](https://guides.rubyonrails.org/active_record_basics.html#migrations)

To run the migration and create the table, you'd run `bin/rails db:migrate`, and to roll it back and delete the table, `bin/rails db:rollback`.
Learn more about [migrations](https://guides.rubyonrails.org/active_record_migrations.html).


## [Associations](https://guides.rubyonrails.org/active_record_basics.html#associations)
Active Record associations allow you to define relationships between models. Associations can be used to describe one-to-one, one-to-many, and many-to-many relationships. For example, a relationship like “Author has many Books” can be defined as follows:

Learn more about the [Active Record Associations](https://guides.rubyonrails.org/association_basics.html).


