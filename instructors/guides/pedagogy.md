# Pedagogy Guide
This guide will provide you with the necessary information to begin the actual writing process of your frontend/backend course.

## Basic guidelines

#### Follow the same chapter layout as the example courses (H1's only)
The example courses are the Angular and Rails courses for frontend and backend, respectively. The general goal is to make it easy for the learners to compare/contrast frameworks, and having a standard learning path through all of them will help with this. The actual contents of each chapter (including subheadings like h2,h3, etc) are fair game to change, although any symmetries you can provide to the example courses (even if you just use the same subheading titles) are ideal.

#### Use checkboxes for tasks
Any time you're having the user do something (whether reading a blog post or modifying a file in the codebase), have the action appear inside a checkbox to ensure they actually do it. The markdown syntax for using checkboxes is as follows:

```markdown
{x: checkbox-name-here}
The markdown placed right after the checkbox (aka the text you're currently reading) will show up inside of the checkbox.

This text, however, will not show up inside the checkbox because there's a space above it.
```

Only use paragraphs inside of checkboxes - it might break if you use a heading, image, etc. We'll probably update this soon, but for now, just use paragraphs (which can contain links, bold, italics, etc).

#### Break H1 chapters into as many relevant subheadings as possible (H2,H3,H4,H5)
We need to do this ourselves for the example courses, but basically the idea is that any specific explanations/tasks should be intelligently grouped to ensure we don't have "run-on" courses. This will also ensure that the learner knows exactly what they're learning/doing at any given time.

## Getting started

Assuming you have the final codebase completed, the process of creating the course looks like this:

1. Break the codebase into chapter by chapter checkpoints, based on the chapter outline. We recommend creating a new github repo and having different branches for the completed code of each chapter.
2. Go through each chapter's completed code and create the step by step instructions to recreate the code that each chapter ends with.
3. Fill in all of the relevant explanations between the step by step instructions.
4. Proof read the course, submit to us for testing!

We are more than happy to help with explaining concepts and getting our hands dirty with testing the courses. Feel free to lean on myself (Eric) and Pai whenever you have questions, need help, etc.
