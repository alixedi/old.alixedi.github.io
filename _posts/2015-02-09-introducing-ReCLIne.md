---
layout: post
title: "ReCLIne - Not a framework"
date: "2015-02-09T14:25:27+00:00"
tags: 
  - python
  - GUI
  - CLI
published: true
---

So you have a quick-and-dirty Python script that normalizes the data in a spreadsheet - the kind that is loved by the Excel-toting suits and (hush!) gets written in a 30 minute post-lunch session while reading hacker news etc.

It so happens that the pudgy fellow from sales - Bob wants to use it. As a responsible if lazy citizen of the Python universe, what are your options? Remember, your fundamental concerns are the following:

1) Bob using your script
2) Not having to work for it



Option-A
--------

* Install Python on Bob's MS Windows laptop.
* Install the various dependencies on Bob's MS Windows laptop.
* Teach Bob that there is a thing called `terminal` and it has nothing to do with disease, cures and people dying for that matter.
* Teach Bob how to run the thing on the (newly discovered) terminal thing. For instance:
  * You: Just type `$ python go-baby-go.py <my_spresheet>`
  * Bob: [`$ $ python...`] It's SHIT!
  * You: Don't type the `$` Bob!
  * Bob: [`$ python go-baby-go.py <my_spreadheet>`] It's SHIT!
  * You: Sigh! I'm coming over.
  * Bob: Right! Why can't you just make it like Excel.


Option-B
--------

* Pick up some random Python GUI library
* Please don't. Do you have any friends? Seriously?


Option-C
--------

* ReCLIne like a Boss!
* "And it even runs on my phone!" - [#SaidBob](http://twitter.com/#SaidBob)


How do I get started?
---------------------

* git clone http://github.com/alixedi/recline
* cd recline
* python recline.py tests/test_ac.py
* Go to your browser and type: localhost:8080
* Enjoy!
* I am working on the PyPI thing.


Technical Stuff
---------------

Not much. I just discovered one fine day that the `argparse.ArgumentParser` object has more information than some half-decent encyclopedias. Thought it would be cool to render web forms from it.
