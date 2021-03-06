---
layout: post
title: Authentication & Authorization
order: 135
---

One of the first serious issues that are usually not covered by a framework is an authentication. In the Rails world, people tend to take the well known Devise lib, integrate it into the app with `devise :database_authenticatable, :registerable`, and forget about auth. That is, until the awkward moment when you need to customize any tiny aspect of it - anything from templates to auth logic (the latter is harder).

The truth is, you can implement auth by yourself very quickly. Just create a users table with login and password fields, encrypt the password with something like the `bcrypt-ruby` gem, store the hashed password in the DB, and write 3-5 controller actions to handle forms. Your users table will not be cluttered with lots of unknown fields, and you will have an idea of what they are for (or you can rely on these fields for other business logic).

A less obtrusive, but still more automated, option is to use Sorcery. Another option is the Tyrant gem – part of the Trailblazer philosophy – that tries to use just a single field of a model.

The fewer hidden pieces of data flow in your app, the easier it is to track down errors and change behavior. In such a sensitive part of the app as authentication, this is very important.

* [Devise](https://github.com/plataformatec/devise)
* [**Sorcery**](https://github.com/NoamB/sorcery)
* [Tyrant](https://github.com/apotonick/tyrant)
* [rodauth](http://rodauth.jeremyevans.net)

Once users can be identified inside the app, the second requirement is to distinguish their abilities. One approach is to assign a marker for each user, like `role = 'admin'`, and check this model attribute all over the app. This is not flexible, however, and when your permission rules change, it requires changes to many different parts of the codebase. Permission logic can be quite complicated, so it should be encapsulated. A good example of simple authorization logic organization is Pundit.

Unfortunately, I do not know of a good example of [RBAC](https://en.wikipedia.org/wiki/Role-based_access_control) implemented in Ruby. The [piece](https://github.com/ThoughtWorksStudios/piece) gem comes close, where roles contain sets of permissions, and all of them can be assigned to a user dynamically with business rules (rules should be implemented as code that checks restrictions).

* [**Pundit**](https://github.com/elabs/pundit)
* [CanCanCan](https://github.com/CanCanCommunity/cancancan)
* [kan](http://github.com/davydovanton/kan)
