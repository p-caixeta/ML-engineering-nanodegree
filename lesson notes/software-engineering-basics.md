# INTRO
The first lesson of the course was "Software Engineering Practices". The objective was to give a few tips to write a more clear and easy to maintain code. 
Below there are the main remarks from this part of the course.

## Software Engineering Tips and Good Practices: 

* Production Code: A software running on production servers to handle live users and data of the intended audience. Note that this is different from production quality code, which describes code that meets expectations in reliability, efficiency, etc., for production. Ideally, all code in production meets these expectations, but this is not always the case.

* MODULE: a file. Modules allow code to be reused by encapsulating them into files that can be imported into other files.

* DRY principle: Don't Repeat Yourself!

* It is ok to first go straight to put the code to run. But as it develops and grows, you should go organizing it 

* REFACTORING: restructuring your code to improve its internal structure, without changing its external functionality. This gives you a chance to clean and modularize your program after you've got it working.

* When using booleans, you can prefix with *is_* or *has_* to make it clear

* Limit your lines to around 79 characters, which is the guideline given in the PEP 8 style

* One functions should do one thing. If a function is doing multiple things, it becomes more difficult to generalize and reuse. Generally, if there's an "and" in your function name, consider refactoring.

* Use vector opeations (numpy and pandas) instead of lists

* Use SETS when iterating to find single ocurrences

* Git: use *git log* to get the commit ID, then *git checkout ID* to read a previous version of the code. If that is the desired version, *checkout* and then *merge*

* TEST DRIVEN DEVELOPMENT: a development process where you write tests for tasks before you even write the code to implement those tasks. You should write tests before you write the code that’s being tested.

* UNIT TEST: a type of test that covers a “unit” of code, usually a single function, independently from the rest of the program.

* Pytest: to install pytest, run pip install -U pytest in your terminal. You can see more information on getting started https://docs.pytest.org/en/latest/getting-started.html.

* Choose the appropriate level for logging

-- DEBUG: level you would use for anything that happens in the program.

-- ERROR: level to record any error that occurs

-- INFO: level to record all actions that are user-driven or system specific, such as regularly scheduled operations

* Object-Oriented Programming (OOP) Vocabulary

-- class: a blueprint consisting of methods and attributes

-- object: an instance of a class. It can help to think of objects as something in the real world like a yellow pencil, a small dog, a blue shirt, etc. However, as you'll see later in the lesson, objects can be more abstract.

-- attribute: a descriptor or characteristic. Examples would be color, length, size, etc. These attributes can take on specific values like blue, 3 inches, large, etc.

-- method: an action that a class or object could take

* encapsulation - one of the fundamental ideas behind object-oriented programming is called encapsulation: you can combine functions and data all into a single entity. In object-oriented programming, this single entity is called a class. Encapsulation allows you to hide implementation details much like how the scikit-learn package hides the implementation of machine learning algorithms.

## Packages in Python

- Python package needs an init.py file inside the folder, and a setup.py file outside the folder

- A Python module is just a Python file containing code.

- A Python package does not need to use object-oriented programming. You could simply have a Python module with a set of functions. However, most if not all of the popular Python packages take advantage of object-oriented programming for a few reasons.  Object-oriented programs are relatively easy to expand especially because of inheritance and OOP obscure functionality from the user (consider scipy packages - you don't need to know how the actual code works in order to use its classes and methods).

- Reminders:

-- Include a README file detailing the files in your package and how to install the package.

-- Comment your code - use docstrings and inline comments where appropriate.

-- Refactor code when possible - if you find your functions are getting too long, then refactor your code!

-- Use object-oriented programming whenever it makes sense to do so.

-- You're encouraged to write unit tests! The coding exercises in this lesson contained unit tests, so you can use those tests as a model for your package.

-- Use GitHub for version control, and commit your work often.

-- As a reminder, your package should be placed in a folder with the following folders and files:

-- * A folder with the name of your package that contains:

-- * The Python code that makes up your package; a README.md file; an init.py; license.txt; setup.cfg; setup.py file

* PyPi vs. Test PyPi: Note that pypi.org and test.pypy.org are two different websites. You'll need to register separately at each website. If you only register at pypi.org, you will not be able to upload to the test.pypy.org repository.

* Unique Name: your package name must be unique

* Re-uploading and Versioning: Once you upload your package to PyPi, you cannot upload the same version again. All that means is that you need to go into your setup.py file and change the version number. For example, if you uploaded a package with version = 0.1.1, then you'll need to change this to something else like version = 0.1.2.
