# How to organize scripts and projects

Answers to a few questions about script and project structures.

## Script headers and descriptions

> What should be included in the header for a script?

My guidance on what is expected in the headers of the scripts might not apply because I'm not in academia and don't write R anymore. That said, if I were to come to a script I'd want to know a few things:

- Why are we running this analysis?
- A brief description of the data, aka the inputs to the script
- A brief description of the analysis, aka the outputs of the script

These are the standard things that code documentation usually covers and they give a good overview of what is happening in the script. For something that is just for yourself, I think this matters less, but it's still nice to have a small description if the script is complex enough.

> What are your thoughts on outlining/creating a table of contents in scripts?

If these are easy to make, and they help you and whoever you're sharing the scripts with, then go for it :) I often use outlines to help organize my thoughts while I'm writing code, and I do sometimes keep them around after the code is written to help readers know the flow.

> What are your thoughts on commenting vs R Markdown?

I hadn't heard about R Markdown before, so I'd like to hear from others what they think and then perhaps I can comment on what I think.

## Scripts that share data

> I am using the same dataset across multiple statistical analyses that will lead to different manuscripts. Should these projects share the data? Is there a good way to share data across projects?

In the case that you have described, I think having each project hold its own copy of the data is fine. I assume the dataset doesn't change very often, if ever, so it shouldn't be a burden to keep each up to date. If the dataset were to change frequently, it might make your life easier to nest the projects as siblings inside a single GitHub project:

```
/project-root
├── analysis_one/
│   └── script_one.rmd
├── analysis_two/
│   └── script_two.rmd
└── data.csv
```

where `script_one` and `script_two` each read in the data like `read_csv("../data.csv")`.

## Script length

This is a classic debate. There are some people out there who try to impose strict limits, like a function definition should only be 10 lines long. I think these enforced limits are too tough; what matters is readability and to achieve that I value organization and focus over length.

**Organization** is typically done with functions or code comments. For example you could have a block of code that reads and preps a data file inside a function called e.g. `readAndPrepData` or just have the lines of code be commented about what they're doing.

To have a script have a **focus** is for it to have an understandable set of goals that are tightly linked. There is a coding philosophy of "Do one thing well" that loosely applies here.

We can use the script that Joel sent as an example.

In it, lines 88 through 436 are defining models. That's a lot of lines, but it's organized under a header of `# Model functions`, and the next section has its own header, `# Model comparisons`. This feels good organizationally to me.

However, I think, and it sounds like Joel thinks this as well, that the script is losing its focus. When the second variable was added, it didn't add to the script's original purpose. If you want to share code between disparate tasks, that's usually a good time to break things up. I would probably structure this with three files:

1. Define the models
2. Import the models and run them on the Self Compassion variable
3. Import the models and run them on the AAQc variable

This makes each file focused and helps the project be extended more easily. If you wanted to run things on a third variable, you could then just add a new file that imports the models and runs them on a particular variable, and the other two would continue to be coherent.
