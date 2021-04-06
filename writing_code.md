# Writing Code. Make it work and then make it human

## Make it work

> You can't edit a blank page.
>
> — V.E. Schwab, author

First focus on making the code do what it is supposed to do and pay very little attention to style or maintainability.

One of the best parts of programming computers is that they are typically deterministic: given the same inputs, a program will generate the same result. We can use this to our advantage to iterate quickly. Here is a flow I use often:

1. Hack together something that works, no matter how ugly.
2. Test your code often. It is helpful if its efficacy can be tested quickly, so maybe use a subset of data if the files to be read are large.
3. Whenever things are working, commit to version control. This is a great way to ensure it is always possible to get back to a working version.
    - See [Version Control](/version_control.md) for how to commit and revert.
4. Now that the code works, iterate on making it human readable (see next section). After each change, test that it works and commit it to version control if it does.

## Make it human

Every piece of code has at least one collaborator, your future self, and many have other collaborators such as current or future teammates.

Despite programs being written for computers to execute, as coders we are also writing for each other. It is worth investing in your future understanding by spending some time now to make things more readable.

There are many opinions about code structure and style, but these are a few patterns that I always try to follow.

### 1. Use words to describe what is going on

It can be tempting to use short variable names like `a` or `b`, or to write complex logic tersely, but this can be hard to understand when revisiting code out of context later. Using descriptive names, or explaining what is going on with code comments, goes a long way to making your future self understand what you write now.

Here's an okay example:
```R
data = read("survey_results.csv")

m = 0
for (r in data) {
  v = r[2]
  if (v > m) {
    m = v
  }
}
```

And a better example:
```R
survey_results = read("survey_results.csv")

# Find the maximum sentiment value, which is in column 2
max = 0
for (row in survey_results) {
  sentiment = row[2]
  if (sentiment > max) {
    max = sentiment
  }
}
```

### 2. Don't reassign variables unless necessary

Programs can be long files and keeping track of what each variable means can be difficult. Reassigning a variable can make things hard to follow.

```R
data = read("survey_results.csv")

result = some_analysis(data)

# Lots
# and
# lots
# of
# very
# cool
# code
# here
# ...

data = read("trial_results.csv")

# More
# of
# the
# best
# code
# ever
# written
# ...

result = a_different_analysis(data)
# wait... which `data` are we talking about?
```

A better solution could be to call the first one a descriptive name like `survey_results` and name the second `trial_results`.

This can be true for any type of value you're assigning to a variable, not just datasets.

One time when you may want to do this is if you're dealing with multiple very large datasets. If the program is using too much memory, only keeping one dataset attached to a variable at a time may help.

### 3. Compartmentalize tasks

A script is a series of instructions to achieve a goal. Remembering this while writing can help make it easier to expand on a particular section.

For example, let's say we're going to read some data, calculate some metrics about it, and then present those metrics.

```R
survey_results = read("survey_results.csv")

average_sentiment = average(survey_results)
print("The average is #{average_sentiment}")

max_sentiment = max(survey_results)
print("The max is #{max_sentiment}")

min_sentiment = min(survey_results)
print("The min is #{min_sentiment}")
```

In the above example, we have optimized for finding a single value and presenting it. While this may be what makes the most sense in some cases, I consider the tasks of analyzing data and presenting data to be different enough that they should be separate.

To see how this can be helpful, let's move all of the presentation code to be together.

```R
survey_results = read("survey_results.csv")

# Analyze survey results
average_sentiment = average(survey_results)
max_sentiment = max(survey_results)
min_sentiment = min(survey_results)

# Present results
print("The average is #{average_sentiment}")
print("The max is #{max_sentiment}")
print("The min is #{min_sentiment}")
```

By separating the analysis code and presentation code, we can see which parts of our program are doing what and can update them apart from one another. For example, let's change the presentation to output a table.

```R
survey_results = read("survey_results.csv")

# Analyze survey results
average_sentiment = average(survey_results)
max_sentiment = max(survey_results)
min_sentiment = min(survey_results)

# Present results
output_table(
  ["Average", average],
  ["Max", max],
  ["Min", min],
)
```

### 4. Only leave in code that is being used

Unused variables or tasks that calculate something that is not used can be confusing when returning to a program. It's find to keep a separate document with notes about things that you tried and didn't end up using, but keeping the code clean of unused items will help you and your collaborators understand what is important and what is not.
