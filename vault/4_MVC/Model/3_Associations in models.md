# 2. Associations in models
### Why associations?
FIXME

### How do they work?
FIXME

### What are associations?
- Forget about tables and databases. Just think about pieces of data (objects).
- There are 4 kinds of associations:
	1. One to one. Example: `user_cred` and `user_profile` on a site. May be unidirectional or bidirectional.
	2. One to many. Example: `user` and `story` on YouTube.
	3. Many to many. `user` and `subreddit` on Reddit.
	4. Polymorphic one to many.

#### What are associations?
- Ignore one to one, as they may be thought of breaking a table down into two tables (just for decreasing table size).
- But many to _ are used when a list of objects may be needed while quering and so, a JOIN operation may need to be performed. That's all there is to it. **Specifying associations indicates JOIN to the Rails ORM, which generates queries based on ActiveRecord::Base**
- When a resource is deleted, related resources have to deleted manually. This is bad design. Using associations makes it very easy, as all related/dependent resources are deleted automatically.

###### Syntax in Rails
- Suppose two model that need an association exist. After [generating](obsidian://open?vault=rubyon-rails&file=3.%20Scaffolding), the model classes are empty.
- Specify relation in the class. Like so:

```ruby
class User < ApplicationRecord
	has_many :stories # one side of the relation
end

class Story < ApplicationRecord
	belongs_to :user # many side of the relation
end
```
- The syntaxes are:
	- One to one: 
		- `has_one`: creates FK in residing model.
		- `belongs_to`: creates FK in target model.
	- One to many: `has_many` with `belongs_to`
	- Many to many: 
		- `has_and_belongs_to_many` for both.
		- `has_and_belongs_through`
FIXME
- Of course, a model may be related to multiple *other* models.]

###### Using associations
Every assoication is like an instance variable now. Just use dot notation. 
- The names of instance variables are singular or plural as per the assoication.
- Direction matters: for unidirectional associations, only one side can use va 
```ruby
@user = User.find(params[:id])
@posts = @user.microposts # plural for many
```


## Questions
- has_many or has_one and belongs to, do they need to be complementarily used. - No, using both will have a bi-directional knowledge, but using one will not.