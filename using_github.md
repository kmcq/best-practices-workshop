## Questions about using GitHub

#### Is GitHub would work for managing writing papers with collaborators? We currently use the "save 10000 versions with different endings" method which seems bad.

This depends on the type of document and your collaborators' familiarity with GitHub. My team does technical writing together and we collaborate using [GitHub Pull Requests](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests). However, git and GitHub are not very good at dealing with complex document types like Word documents or PDFs. In addition, anyone you collaborate with would need to be proficient in using GitHub. For collaborating on code, using GitHub is stellar.

#### Are the fancy features of GitHub (wikis, issue tracking, etc) useful for personal use or mostly if you are working on teams?

For personal projects, I sometimes use them and it depends on the complexity of the project. If I want to have ways to keep track of my notes and progress for a task, then I'll use issues and projects.

I find features like issue tracking are essential for working with a team. GitHub issues allow for teammates to discuss specific aspects of a project; for example you could have an issue about how to collect data and another about discussing different analysis techniques.

For a smaller project, a strategy I use often is to-do lists within my code as code comments. I then fill in the pieces and delete the to-do items. For example:

```ruby
def read_and_analyze_data
# TODO: read in data
#   - Figure out how to do this in a performant way.
# TODO: run the data through a random forest regression
#   - Which library should we use to do this?
end
```

I don't use the wikis feature. I like to have my documentation live next to the code I write so that I can more easily edit the documents on my laptop, away from the web browser.
