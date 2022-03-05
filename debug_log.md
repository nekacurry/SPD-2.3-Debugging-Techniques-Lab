# Debug Log

**Explain how you used the the techniques covered (Trace Forward, Trace Backward, Divide & Conquer) to uncover the bugs in each exercise. Be specific!**

In your explanations, you may want to answer:

- What is the expected vs. actual output?
- If there is a stack trace, what useful information does it contain?
- Which technique did you use, on which line numbers?
- What assumptions did you have about each line of code, and which ones were proven to be wrong?

_Example: I noticed that the program should show pizza orders once a new order is made, and that it wasn't showing any. So, I used the trace forward technique starting on line 13. I discovered the bug on line 27 was caused by a typo of 'pzza' instead of 'pizza'._

_Then I noticed another bug ..._

## Exercise 1

When going to submit an order, the site responded with TypeError: 'topping' is an invalid keyword argument for PizzaTopping. I used the Divide and Conquer technique and searched for instances of PizzaTopping and topping in attempt to find the bug. For adding the pizza toppings on line 79, it had .append(PizzaTopping(topping=topping_str)), but the PizzaTopping class does not have an attribute of "topping", so I changed it to topping_type to fix the error. 

Now when submitting an order, you get the error "werkzeug.routing.BuildError: Could not build url for endpoint '/'. Did you mean 'fulfill_order' instead?" On line 84, the url redirects to '/'. I used the trace forward method to understand how the code is supposed to navigate, and changed '/' to home, as it should be redirecting to an html file instead of a route.

Now that the order sceen redirects properly, the orders on the home page don't show! I used Divide and Conquer to check if the information of the pizza orders where being pushed anywhere, they weren't, so I added a new line on 82 to update the database. 

From here I received another error that didn't include the toppings on the pizza when submitted, so on line 76, I added the list of toppings to the Pizza object.

From here I recieved "AttributeError: 'tuple' object has no attribute 'size'", I went back to look at the order function, and on line 68 it requests "size" from the form instead of "pizza_size" as it is in the html, so I changed it accordingly, then did the same ting with order_name. 

Now it works!



## Exercise 2

I started off by running the app and when submitting the inputs on the form, I recieved and Internal Server Error and traced backe to line 52, where it wasn't finding a name for the city. Tracing back up farther to line 39, it was written as "user_city" instead of city. Through this i also found that the units were incorrectly written as "requested_units". 

I also found that in the params on line 45, city should be replaced with "q" instead (I've worked with this API before!). This then made me check if the API was being called properly, so on line 44 I properly called the API from the .env file. 

From here there is now a KeyError with temperature. Checking the API docs, temperature should be "temp" instead, so I then changed line 54.

Now it works!

## Exercise 3

Running the code initially gave an IndexError that the list index is out of range in the merge_sort function. Tracing back to line 37, the index was i when it should have been j. 

Next there was a TypeError in the binary_sort. The list indice was returning as a float instead of an integer or slice, so I traced back and changed line 48!

Now it works :)
