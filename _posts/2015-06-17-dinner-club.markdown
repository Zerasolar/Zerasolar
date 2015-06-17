---
layout: post
title:  "Dinner Club"
date:   2015-06-17 09:11:37
categories: code
---

Dinner Club markdown I wrote for class

# Dinner Club

It's a program that takes the users inputs of locations, names and amounts for going out and keeps them as records for the dinner club. It also utilizes the Checksplitter method to split a check between the members if they need to.

We set up an initialize method that uses the member_name as an argument with the members hash that holds the name of the attendees and the amount that each member had paid for the duration of being a member of the club. With the members hash
that we had to make sure that each attendee in the group had started at 0 when the attendee first join. We have a history array which will store the event hash. With that event hash stores the name of the restaurant and the attendees who went to the event.

```ruby
 def initialize(member_names)
    @members = {}
    @history = []
    member_names.each do |name|
      @members[name] = 0
    end
  end
 ```
The first method that listed is event which is part of the history array. The event method is a hash that holds the names of the restaurant the members of the group had dined at and the attendees who went to the event.

```ruby
  def event(restaurant, attendees)
    event = {}
    event[restaurant] = attendees
    event
  end
  ```
The go out method uses total_cost_of_meal, tip_percent, attendees, yes_no, treater as the parameter. Next is the if statement to see if someone is treating the whole group. If the input is a "no" or "" or a nil we continue down the code to use the other class called 'CheckSplitter' since the group is splitting the check.

```ruby
def go_out(total_cost_of_meal, tip_percent, attendees, yes_no, treater)
    
    #if treater is nil or no then the group is splitting the whole bill

    if yes_no == nil || yes_no == "" || yes_no == "no"
```
'CheckSplitter' takes the input information and calculates the total cost of the meal, what percentage they are tipping the server and how many people are in the group to split the check of the meal. From that we now know how much each person has to pay. Which then the name of the member and how much they had to pay is store in the members hash.

```ruby
      cs = CheckSplitter.new(total_cost_of_meal, tip_percent, attendees.length)
      amount_per_person = cs.split
      attendees.each do |a|
        @members[a] = @members[a] + amount_per_person.to_f
      end 
 ```
 
If someone is treating the whole group then the program goes to the else statement runs through the 'CheckSplitter', but now it is only to get the total of the meal and the tip added together. Next it updates the member listing of who all attended, but only updated the amount person who treated the group.  

```ruby
    else
      cs = CheckSplitter.new(total_cost_of_meal, tip_percent, attendees.length)      
      totalvalue = cs.totalvalue
      @members[treater] = @members[treater] + totalvalue.to_f   
    end
  end
  ```
The last method is 'history' an array that will be storing the place that the group went to and the attendees who went by having the event hash being pushed into the history array to be stored. The event hash has the restaurant that the attendees went to and the attendees that joined for that event.
  
 ```ruby
      def history(place, attendees)
      
  @history.push(event(place, attendees))     
   
    end
    
    @members
  end      
 ```
 