---
layout: post
title: CP-Sat vs Simple DFS
date: 2024-01-01
categories: programming algorithms
---
SAT solvers have a reputation for indistinguishable-from-magic performance when solving hugely complex problems. Ideal for solving a brain-puzzler from [a 7 year olds puzzle book](https://www.amazon.co.uk/Intermediate-Logic-Workbook-Gritty-Kids/dp/B0CTYQ1JGR).
![Page 40 of Intermediate Problems for Gritty Kids](/assets/images/puzzle.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

### Python Solution
[Code on GitHub https://github.com/engie/hgridsolve/blob/main/hgridsolve.py](https://github.com/engie/hgridsolve/blob/main/hgridsolve.py)
{% raw %}
<iframe frameborder="0" scrolling="no" style="width:100%; height:357px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Fengie%2Fhgridsolve%2Fblob%2Fmain%2Fhgridsolve.py&style=default&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on&maxHeight=300"></iframe>
{% endraw %}
* The 3x3 grid of cells represented as a list, where each value is an array of what animals could be in that cell.
* Some of the more absolute rules are initially applied to narrow down possibilities.
* A recursive depth first search runs:
  * First applying rules to cut down possibilities
  * If this ends up with no possibilities for a cell, then return failure
  * If this finds one possible value for each cell, then return success
  * Otherwise build a list of guesses, where a cell is fixed to one of the possible values. For all of these guesses, try building a grid with that fix applied and recurse.

#### Pros
* All done with simple Python code, readable by millions. Illegibility the responsibility of the author.
* Fairly easy to debug as the rules can be stepped through as they're applied recursively, with all state visible.

#### Cons
* Pure brute force - the search doesn't learn anything as it goes, it's just working its way through all the possible answers. This is obviously fine for this small scale, it executes instantly, but is limited. But computers are fast!
* Boring, no need to write a blog post about it.

### [CP-Sat](https://developers.google.com/optimization) Solution
[Code on GitHub https://github.com/engie/hgridsolve/blob/main/satsolve.py](https://github.com/engie/hgridsolve/blob/main/satsolve.py)
{% raw %}
<iframe frameborder="0" scrolling="no" style="width:100%; height:357px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Fengie%2Fhgridsolve%2Fblob%2Fmain%2Fsatsolve.py&style=default&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on&maxHeight=300"></iframe>
{% endraw %}
* Each cell is setup as a CP-Sat IntVar, with the numbers 0-8 representing the different animals, forced to be different with AllDifferent. This is where the solution ends up.
* Each rule is turned added to the model as either a fixed value for a cell, allowed/disallowed combinations of values between cells, AtMostOne rules, AddExactlyOne and lots of bools that go true when certain cells take specific values.
* Some rules end up more complicated, with int or bool vars added to the model to represent e.g. the number of times certain values appear in a column.
* A couple of helper functions make it easier to create intermediate vars, and I'm not sure if this is a good idea.
* The solver is triggered, and the result can be retrieved.

#### Pros
* I'm assured this solver could tackle applying a vast number of complex rules to a huge number of variables, using arcane tricks to build its own intuitions about where to go looking for a solution. If I understood this better I'd refer to things like simplex algorithms etc.
* If there were multiple possible solutions the solver could try to find more optimal ones, building intuitions for how to increase its score.

#### Cons
* Building the more complex rules like "Beaver and Eagle share a column" required some lateral thinking, consultation with Prof. GPT and lots of extra variables added to the model. I'm not at all sure the solution I ended up with is in any way good, it feels pretty over the top for the task at hand. I don't have a strong intuition for when it's best to add intermediate variables.
