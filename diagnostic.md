# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

```txt
  There are instances in which tables share data points. For example, in my project, in order to reduce amibiguity, assignments are made by user ID rather than the user itself because the ID is totally unique.
```

1.  Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
`Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
join table with references to `Movies` and `Profiles`.

```txt
  A profile has many movies and favorites while. Movies belongs to favorites and favorites has many movies and belongs to one profile.
```

1.  For the above example, what needs to be added to the Model files?

```rb
class Profile < ActiveRecord::Base
has_many :movies, :favorites
end
```

```rb
class Movie < ActiveRecord::Base
belongs_to :favorites
end
```

```rb
class Favorite < ActiveRecord::Base
has_many :movies
end
```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

```txt
  A serializer is like a filter. It dictates what the user can and cannot see.
```

```rb
class ProfileSerializer < ActiveModel::Serializer
:title, :release_date, :length
end
```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

```sh
  bundle exec rake g scaffold AddMovieToFavorites title:reference
```

1.  What is `Dependent: Destroy` and where/why would we use it?

```txt
  This is a feature than ensures when one part of a table is deleted all other associated data is removed as well. So, if a user is deleted, so are all of their movies and favorites as opposed to having leftover data as artifacts.
```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

```txt
  In my application a user is assigned chores. One user has many chores asssigned to them.
  A many to many relationship could be a lawfirm and clients. Corporations have many lawyers that handle their operations while those lawyers probablye have many clients.
```
