---
layout: docs
title: Models
permalink: /docs/models/
---

## Model Declaration

To create a model with NoBrainer, simply include the `NoBrainer::Document` mixin
in your class as such:

{% highlight ruby %}
class User
  include NoBrainer::Document
end
{% endhighlight %}

There is no migrations needed to use the model since NoBrainer creates the
required tables for you by default.

The default table name is `class.name.tableize.gsub('/', '__')`.
You may change the table name as described in the
[Multi Tenancy](/docs/multi_tenancy) section.

## Polymorphic Models

To use polymorphic models with single table inheritance, simply inherit your
classes. Example:

{% highlight ruby %}
class Admin < User
end
{% endhighlight %}

NoBrainer uses a `_type` attribute in the subclass documents to be able to query
and instantiate the proper classes.

Note that when using Rails, you might have to use `require_dependency` to ensure
that all subclasses are loaded. See more in the Rails guide,
[Autoloading and STI](http://guides.rubyonrails.org/autoloading_and_reloading_constants.html#autoloading-and-sti).

## Reflection

Sometimes it's useful to go through all the models to do something fancy.
The list of models can be retrieved with `NoBrainer::Document.all`.
When using polymorphism, note that subclasses are not returned, only root classes.
