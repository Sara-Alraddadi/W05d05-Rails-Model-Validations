# Rails Model Validations

## Objectives

By the end of this lesson you should be able to...

- Know, what is validation and why we need it
- Add validations to our models

## Introduction

Active Record allows you to validate the state of a model before it gets written
into the database. There are several methods that you can use to check your
models and validate that an attribute value is not empty, is unique and not
already in the database, follows a specific format and many more.

Validation is a very important issue to consider when persisting to database, so
the methods `create`, `save` and `update` take it into account when
running: they return `false` when validation fails and they didn't actually
perform any operation on database. All of these have a bang counterpart (that
is, `create!`, `save!` and `update!`), which are stricter in that
they raise the exception `ActiveRecord::RecordInvalid` if validation fails.

Let's look at how we might validate some things.

-   **Empty Values**

      To prevent empty values we'll use `validates <property>, presence: true`.
      This is a slightly more restrictive check than `null: false`;
       it disallows both empty values (`nil` in Ruby, `NULL` in the database),
       and it also disallows empty strings (for string properties).

      **EXAMPLE :**
      To set an empty-value validator in our Dcotors model, you might write

      ```ruby
      class Doctor < ApplicationRecord
    has_many :appointments
    has_many :patients, through: :appointments
    validates :name, presence: true
      end
      ```

-   **Uniqueness**

      To ensure that a property is unique,
       we'll use `validates <property>, uniqueness: true`.

      **EXAMPLE :**
      To set some uniqueness validators in my Person model, you might write

      ```ruby
      class Doctor < ApplicationRecord
    has_many :appointments
    has_many :patients, through: :appointments
    validates :name, presence: true, uniqueness: true
      end
      ```

<br>
<hr>
`ActiveRecord::Base` comes with a slew of other validators we can use, as well as the mechanisms to create our own custom validators.
<hr>
<br>

-  **Only Alphabets**

      ```ruby
      class Doctor < ApplicationRecord
    has_many :appointments
    has_many :patients, through: :appointments
    validates :name, presence: true, uniqueness: true, format: { with: /\A[a-zA-Z]+\z/,
     message: "only allows letters" }
      end
      ```

<br>
<hr>

-  **Only Numbers**

      ```ruby
      class Doctor < ApplicationRecord
    has_many :appointments
    has_many :patients, through: :appointments
    validates :name, presence: true, uniqueness: true, numericality: true
      end

      ```

<br>
<hr>

-  **Minimum Length**

      ```ruby
      class Doctor < ApplicationRecord
    has_many :appointments
    has_many :patients, through: :appointments
    validates :name, presence: true, uniqueness: true, format: { with: /\A[a-zA-Z]+\z/,
     message: "only allows letters" }, length: { minimum: 5, too_short: "must have at least %{count} words" }
      end

      ```

<br>
<hr>

-  **Maximum Length**

      ```ruby
      class Doctor < ApplicationRecord
    has_many :appointments
    has_many :patients, through: :appointments
    validates :name, presence: true, uniqueness: true, format: { with: /\A[a-zA-Z]+\z/,
     message: "only allows letters" }, length: { minimum: 5, maximum: 10, too_short: "must have at least %{count} words" }
      end

      ```

<br>
<hr>



You can learn more about validations in the [Active Record Validations
guide](http://guides.rubyonrails.org/active_record_validations.html).


<br>


## Further Reading

* [Active Record Overview - Rails Guides](http://guides.rubyonrails.org/active_record_basics.html)
* [Active Record Migrations - Rails Guides](http://edgeguides.rubyonrails.org/active_record_migrations.html)
* [Active Record Associations - Rails Guides](http://guides.rubyonrails.org/association_basics.html)
* [Active Record Validations - Rails Guides](http://guides.rubyonrails.org/active_record_validations.html)
