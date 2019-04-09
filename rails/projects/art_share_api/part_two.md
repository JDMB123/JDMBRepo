# Art Share API Part 2

## Make sure to finish Phases I - III before continuing!

### Phase IV: Comments

#### Overview

Now it's time to add commenting functionality to our application so our
users can comment on a piece of artwork. By the time we're done, we want
to be able to retrieve both a specific user's comments as well as
comments left on a specific artwork. To do with we'll have our
`CommentsController#index` method return commments based on the params
provided by our request.

### Instructions

First create a comments table that has a foreign key for both user and
artwork. We'll also want a `body` column that contains the text of the
comment. On what columns should we add an index?

Our users and artworks will both `have_many` comments. A comment should
`belong_to` a author (the user who left that comment) and artwork. Write
these associations now. Remember to include `dependent: :destroy` when
necessary. For instance, when an artwork or user is removed from the
database, we don't want their associated comments to persist.

Before moving on test that these associations work.

Once we know our table and model have been set up correctly, it's time
to make our controller. The `CommentsController` should have `create`,
`destroy`, and `index` actions.

In order to retrieve comments for an artwork or a user we want our
`index` action to handle some additional params. In particular, we want
to be able to pass in a `user_id` or a `artwork_id`. By checking if
either is present we can then retrieve the comments just for that user
or artwork. Update your `comment_params` accordingly.

### Recap

It should now be possible to make `GET` requests to
`CommentsController#index` and depending on the params provided either
return comments made by a particular user or comments made on a
particular piece of artwork.

## Phase V: Search

### Overview

Now let's add search functionality to our application so users can
search for other users by name. To do this we won't need to change any
routes. We can just edit the `index` action in our `User` controller.

In `UsersController#index` check if a `query` is present in the request
params. If it is, use that query to filter the users returned by the
`index` action. If there is no query, just return all users as usual.

Discuss with your partner the best way to write your query method.
Here's a [good place to start][postgres-search].

## Bonus Phase I: Likes

In this phase we'll implement likes using polymorphic associations.
Users should be able to like both comments and artworks. Read these
[Rails docs][polymorphic-associations] on polymorphic associations to
get started.

Then discuss with your partner how you plan to approach this feature.
We'd like to be able to call associations on a user and return their
liked comments and artworks. We also want to be able to call an
association on comments and artworks to get the users who have liked
them.

## Bonus Phase II: Favorite Artworks

Let's also allow users to favorite artworks. This will require
additional columns to artworks (for favoriting of artworks by their
owner) and shared artworks (for favoriting of artworks shared to a
user). Use a semantic custom route to accomplish this.
[Hint.][more-restful-actions]

## Bonus Phase III: Artwork Collections

And finally, users should be able to add artworks to artwork
collections. Allow each user to have many collections. Artworks can also
belong to more than one collection. What sort of table will you need to
make this work?

[postgres-search]: https://www.postgresql.org/docs/8.3/static/functions-matching.html
[polymorphic-associations]: http://guides.rubyonrails.org/association_basics.html#polymorphic-associations
[more-restful-actions]: http://guides.rubyonrails.org/v3.2.14/routing.html#adding-more-restful-actions
