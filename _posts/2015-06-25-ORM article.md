---
layout: post
title:  "ORM"
date:   2015-06-25 07:40:37
categories: code
---


#ORM Article

ORM is a Object-relation mapping in computer software. It is a programming technique for converting data between incompatible type system in object-oriented programming languages. It is a tool that lets you query and manipulate data from a database using ruby.

How does my ORM help me get all of a particular table's row from the database. Well we could use the find method to find a particular row if we knew the selected id of the row we want, but if that isn't always the case.

```
  def find(id)
    table_name = self.to_s.pluralize.underscore
    results = DATABASE.execute("SELECT * FROM #{table_name} WHERE id = #{id}").first
    self.new(results)
  end
```

We could use the all to pull of all the rows and then find the one row we need and look that one up. Oh and the best part is that we don't have to just use it for one class, because how it is set the ORM up we can use it with any class we want.

```
  def all
    table_name = self.to_s.pluralize.underscore
    results = DATABASE.execute("SELECT * FROM #{table_name}")
    
    results_as_objects = []
    
    results.each do |result_hash|
      results_as_objects << self.new(result_hash)
    end
    return results_as_objects
  end
  ```

How does my ORM represent rows from a table, given that Ruby doesn't hava a table data structure. It sounds like the all method we used before would work great here which it seaches all of the data. It works great if you need a listing for an object that you need to see what is going on? Though when you use it in your project you will have to set up how your listing should look to the user.
For example for Ruby in HTML listing a class table:
```
<ul>
  <% Good.all.each do |list| %>
  <p><li><%= "#{list.id} - #{list.serial_number} - #{list.distributor_id} - #{list.product_id} - #{list.name} - #{list.description} - #{list.cost} - #{list.quantity}" %></li></p>
  <% end %>
</ul>
````

How does your ORM convert rows from a table to Ruby data structure. Well it depends on what you get from the class. Generally it convert over as an array of hashes that has the object of the class. Again using the all method.

