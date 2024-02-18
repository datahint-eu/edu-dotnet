# The laws of development

## The wisdom I *try* to follow myself

- *I'm an idiot.* Never assume you have all the answers. Research how other people solved similar problems.
- The code you write isn't set in stone, it can and should change if the programming language evolves, your knowledge evolves, ... .
- Don't be embarassed if you write bugs. Even the best developer writes bugs, it's the way you handle *fixing* the bugs that makes you a good developer.
    - Never utter the words 'well, it works on MY machine, so there is nothing wrong with my code'.
	- Debugging is a crucial skill in complex systems. You never learn to debug if you don't write tons of mistakes in the first place.
- Ask questions, understand the domain you are working in.
- Don't make assumptions, they often end up to be wrong.

## Code Guidelines

- Follow the code guidelines set by the team. Try to be consistent.
- First learn to write code accurately, afterwards learn how to do it quickly AND accurately.
- Don't make me think.
    - Code should be easy to read. Don't try to be clever with a one-liner if it is barely readable.
	- Write little pieces of documentation every 5-10 lines to structure your code. Explain in the documentation WHAT you are doing and WHY you are doing it.
	- If you use *magic numbers* (constant values, ...), document WHERE they came from, or even better, move them to a class dedicated to constant values.
	- Think about yourself or the maintainer of the system 5 years later: you won't remember every single detail. Write down your thought process while you write the code.
- Don't reinvent the wheel:
    - Use *good* third-party libraries if they match your needs.
	- Contribute back to open source projects if there features missing that you might need.
    - Understand the basics of open source licenses (MIT, Apache, BSD, GPL, LGPL, AGPL, ...), so you understand if they are compatible with your own projects.
- Write documentation, but not useless documentation. For example:
    - A `Name` property rarely requires any documentation.
	- It might require documentation if the name must adhere to a specific format.
- Be wary about the *latest and greatest*
    - Don't do something because other people jumped ship and appear to be abandoning certain technologies.
	- Microservices are a great example of this in my opinion. There is nothing wrong with a modular monolith.
	- Microservices work for FAANG companies, so a lot of people mistakingly assume it is the answer to all problems, even though they often cause more problems then they are solving if you work in smaller companies.

## General Development Guidelines

- Write unit tests (with mocking) where possible. Remember that most companies don't have the same needs as NASA and don't have the budget for 100% test coverage.
- Use the `AAA` pattern (arrange, act, assert) when writing unit tests.
- Use the right tools for the job:
    - wiki system for documentation
	- ticketing system for work orders and bug tracking
	- CI (continuous integration) system for builds and deployment pipelines.
- Use the *click once* principle for deployment.
    - Your deployment should only be 1 step, or at most a couple of steps.
	- Any complex deployment procedure will fail at some point because the correct order of execution wasn't followed.
- *Business Logic* should be moved to 1 part of the system, so it isn't scattered all over the place.

## Acronyms & Clichés

- KISS: Keep It Simple Stupid
    - Simple code takes less time to write, is easier to understand and debug.
	- As a consequence it will end up with fewer bugs.
- DRY: Don't Repeat Yourself
	- The principle is stated as: *Every piece of knowledge must have a single, unambiguous, authoritative representation within a system*
	- Duplication of code ends up in a maintenance nightmare.
- YAGNI: You Aren't Gonna Need It
    - Write code when you need it, don't try to implement a feature you foresee you might need in the future.
	- Generally, you end up not needing it or the requirements might have changed anyway, forcing you to revisit the code.


TODO: SOLID(link to design principles), Not invented here, Premature Optimization, Boy-Scout Rule, Principle of Least Astonishment
