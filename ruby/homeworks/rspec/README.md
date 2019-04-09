# RSpec Homework

For tonight's homework, we will be implementing some specs for the Dessert class!

Here's what you need to do:

  * Download the [project skeleton][rspec-homework]
  * Review the `dessert.rb` and `chef.rb` files to see what functionality exists.  Do not edit or add any code to these files.
  * In the `dessert_spec.rb` file, implement all of the pending specs (the `it` statements without blocks).  
  *  Run your specs and see that they all pass!

Hints:

You should be using **mocks** for the `Chef` class - don't make actual instances of the `Chef` class! We want to
isolate and test the behavior of the `Dessert` class on its own. If you get stuck, revisit the reading on [creating mocks/doubles][mocks].  Accessing this on GitHub? Use [this link][github-mocks]. The `chef` double has already been created for you, but you will need to add to it!

[rspec-homework]: http://assets.aaonline.io/fullstack/ruby/homeworks/rspec/skeleton.zip
[mocks]: test-doubles
[github-mocks]: https://github.com/appacademy/curriculum/blob/master/ruby/readings/test-doubles.md

**Note:** Technically, this is not Test Driven Development since we've provided the Dessert class for you. That's okay! The idea for tonight's homework is to familiarize you with RSpec syntax and methods. Enjoy your dessert!

