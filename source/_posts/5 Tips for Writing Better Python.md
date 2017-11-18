---
title: 5 Tips for Writing Better Python
date: 2017-10-07 12:53:12 
categories: "Python" 
tags: 
     - Python
description: 5 Tips for Writing Better Python
---

# 1. Make your code a PIP-installable Package
When you come across a new Python package, it’s always easier to start using it if all you have to do is run “pip install” followed by the package name or location.

There are a number of ways to do this, my “go to” being to create a setup.py file for my project.

Assume we have a simple Flask program in “flask_example.py”:

``` python

    from flask import Flask
    app = Flask(__name__)
    
    @app.route('/')
    def hello_world():
    	return 'Hello, World!'
    
    def main():
    	app.run()
    
    if __name__ == ‘__main__’:
    	main()
```

We can turn this into an installable Python package by first moving it into a separate folder (let’s call this “flask_example/”. Then, we can make a setup.py file in the root project folder that looks like this:

``` python

	from distutils.core import setup
	
	setup(
	    name='flask_example',
	    version='1.0',
	    description='Hello, World! in flask.',
	    packages=['flask_example'],
	    install_requires=[
	        'Flask==0.12.2'
	    ],
	    entry_points = {
	        'console_scripts': 'runserver=flask_example.flask_example:main'
	    }
	)
```

This has a few advantages that comes with it. First, you can now install your app locally using “pip install -e .” This makes it easier for developers to clone and install your project because the setup.py file will take care of all the heavy lifting.

Second, with the setup.py file comes dependency management. The install_requires variable allows you to define packages and specific versions to use. If you’re not sure what packages and versions you are using, run “pip freeze” to view them.

<!--more-->

Lastly, this allows you to define entry points for your package, which allows you to now execute the code on the command line by simply running “runserver”.

# 2. Lint Your Code in a Pre-Commit Hook
Using a linter can fix so many problems in code. PyLint is a great linter for Python, and if you’re using a version control system like Git, you can make Git run your code through a linter before it lets you commit your code.

To do this, install the PyLint package.

``` python
	pip install pylint
```

Then, add the following code to .git/hooks/pre-commit. If you already have a pre-commit hook doing something, simple append the pylint command to the end of your file.

``` python

	#!/bin/sh
	pylint <your_package_name>
```

This will catch all kinds of mistakes before they even make it into your Git repository. You’ll be able to say goodbye to accidentally pushing code with syntax errors, along with the many other things a good linter catches.

# 3. Use Absolute Imports over Relative Imports
In python, there are very few situations where you should be using relative module paths in your import statements (e.g. from . import module_name). If you’ve gone through the process of creating a setup.py (or similar mechanism) for your Python project, then you can simply reference submodules by their full module path.

Absolute imports are recommended by PEP-8, the Python style guide. This is because they’re more informative in their names and, according to the Python Software Foundation, are “better behaved.”

I’ve been in positions where using relative imports has quickly become a nightmare. It’s fine when you first start coding, but once you start moving modules around and doing significant refactoring, they can really cause quite the headache.

# 4. Context Managers
Whenever you’re opening a file, stream, or connection, you’re usually working with a context manager. Context managers are great because when used properly they can handle the closing of your file should an exception be thrown. In order to do this, simply use the with keyword.

The following is how most beginner Python programmers would probably write to a file.

``` python

	f = open(‘newfile.txt’, ‘w’)
	f.write(‘Hello, World!’)
	f.close()
```

This is pretty straightforward. But imagine this: You’re writing thousands of lines to a file. At some point, an exception is thrown. After that happens, your file isn’t properly closed, and all the data you thought you had already written to the file is corrupt or non-existent.

Don’t worry though, with some simple refactoring we can ensure the file closes properly, even if an exception is encountered. We can do this as shown below.

``` python

with open(‘file’, ‘w’) as file:
    file.write(‘Hello, World!’)
```

Volla! It really is that simple. Additionally, the code looks much cleaner like this, and is more concise. You can also open multiple context managers with a single “with” statement, eliminating the need to have nested “with” statements.

``` python

with open(‘file1’, ‘w’) as f1, open(‘file2’, ‘w’) as f2:
    f1.write(‘Hello’)
    f2.write(‘World’)
```

# 5. Use Well-Named Functions and Variables
In Python, and untyped languages especially, it can easily become unclear what functions are returning what values. Especially when you’re just a consumer of some functions in a library. If you can save the developer the 5 minutes it takes to look up the function in your documentation, than that’s actually a really valuable improvement. But how do we do this? How can doing something as simple as changing the name of a variable save development time?

There are 3 main things I like to take into consideration when naming a function or variable:

* What the function or variable does
* Any units associated with the function or variable
* The data type the function or variable evaluates to

For example, if I want to create a function to calculate the area of a rectangle, I might name it “calc_rect_area”. But this doesn’t really let the user know much. Is it going to return the value, or is it going to store it somewhere? Is the value in feet? Meters?

To enhance the name of this function, I would change it to “get_rect_area_sq_ft”. This makes it clear to the user that the function gets and returns the area. It also lets the user know that the area is in square feet.

If you can save the developer 5 minutes here and there with some nicely named functions and variables, that time starts to add up, and they’ll appreciate your code all the more.

# Conclusion
These tips are ones that I have found to be helpful over my years as a Python programmer. Some of them I figured out on my own over time, some of them others had to teach me so I could learn them. I hope this list helps you in your effort to write better Python.


via [here](https://michaelwashburnjr.com/5-tips-for-writing-better-python/)