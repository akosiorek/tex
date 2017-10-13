# Research Methods Workshop Notes

## Reading Papers
  * 4 ways to read a paper; you'll really understand only a handful papers during your PhD
  * old paper: follow "cited by" to see if it was done before before starting or to just see what was done in the mean time
  * novelty: go through references to judge the actual contribution; often it's just incremental

### Reviewing Papers
  * be constructive; justify whatever you're saying
  * write reviews you'd like to receive; even if you reject, the authors should know why and how to improve their work

## Reference Management
  * Try not to cite arxiv; you can, but if there is anything available that is peer-reviewed, do that
  * Do not cite Wikipedia

## Learning

### Specific Things That You Need to do Research

  It's natural not to know stuff. Accept it, drop your ego.... drop your ego a bit more... let's start.

#### Mathy stuff
  Using advanced concepts without having the basics is mostly impossible and can be dangerous (can cost lots of wasted time and frustration). Say you wanted to learn about **inference in linear dynamical systems**. There are to ways to go about this:
  * Jump into learning about inference in LDS
  * Learn about probability theory, linear regression, graphical models and then go into LDS

  2) might take you a shorter time than 1), is almost guaranteed to be much more rewarding and much less frustration. Plus, at the end, you will have a pretty good understanding of what's happening in LDS. If you jump into 1) straight away, well, good luck.

#### Programming
  Say you want to code neural nets in Tensorflow but you don't know Python.

  Option 1):
    You know C++, you think you can figure out Python along the way. You grab some advanced Tensorflow tutorials, Cifar-10 with encapsulated model loading etc, and give it a go. You try to modify it to suit your needs, but it doesn't work. You spend a week on it, don't learn a thing, get terribly frustrated.

  Option 2:
    * Grab a thorough Python tutorial or a book and spend 1-5 days learning Python
    * Grab the easiest tutorial on TF you can find, go through it and make sure you understand every single line of code and what it does
    * Try to code your own model in the simplest possible way
    * Go to the advanced tutorial


### General Knowledge Expansion

  It's vital for continual progress. We cannot afford to stop learning, and not only in our main research direction. We need more general knowledge to be better at generating ideas, to find creative ways of implementing those ideas and to see similarities and relations between similar concepts in different fields. It can save us a lot of trouble with reinventing the wheel.

  Couple of things I follow:
  * always have a (non-tech) book to read and read whenever you can; make time for reading
    * Right now I'm reading Pre-Suasion by Robert Cialdini

  * always have a technical book to read or a(n online) course to follow and allocate some time every week to study it
    * I did Bishop's "Pattern Recognition and Machine Learning": 30 min a day, every day
    * I'm starting Barber's "Bayesian Time Series Models"
    * courses available on edX and Coursera

  * have a list of blogs that you read periodically, e.g. allocate time every 2-3 weeks to go through them. Blogs introduce topics less formally and in a shorter and easier to digest way than coursers or books. My favourites are:
    * Ferenc Huszar
    * Shakir Mohammed
    * Andrew Gibiansky

## Note Taking
  * seminars, talks, conferences, ideas: write summaries to consolidate knowledge
  * write ideas when you have them; update notes whenever you think some more or develop some results
    * hint: electronic version is simpler to update
    * notes in md or tex + github, or evernote; I think I prefer github + md for initial/casual and tex for more advanced

## Project Management
  * Make backups!
  * Do set goals, plan for conferences, keep track of timelines
  * Jira is good, Trello is good

## Experiments
  * what is it that you want to figure out about the problem, or what do you want to show?
  * write down the goal of the experiment before starting that
  * keep track of hyperparameters
  * saving the exact code used to run the experiment (with the model code as well) is useful; you can check into git and store commit model
    * even stronger: always run an experiment from a commit with a known hash that you save in your results file
  * google sheets is a good place to store experiment results
  * after the experiments: have you learnt anything? If not, it means you've done something wrong
    * even then, you can turn it into a learning experience by asking: why is it I haven't learnt anything? what went wrong? find out and you will not make that error again
  * those results will go into a thesis one day and you need to keep the results together with the code and be able to re-run stuff later possible on other data sets. Why? Because it's all about the narrative and you might need code to reframe it.
  * the fear: you have to always fear that whatever you tell the world is wrong. Performs a lot of sanity checks just to check what you think is right is actually right. If you don't, you're in trouble.

  ### Baselines
  * it's important to know how the current SOTA or even a simple method performs on the task
  * start your experimenting by first implementing a baseline, only then work on your own crazy complicated model and show that it outperforms the baseline; if it doesn't, there's not point telling the world about it, unless (fill in the blank)


## Thesis Planning
  * Set up a thesis skeleton with structure and chapters before 3rd year
  * Make timelines when you want to finish what (both experimenting and writing) and where you want to publish Things
  * Organise workflows into periods preceding conferences
  * Go do stuff
