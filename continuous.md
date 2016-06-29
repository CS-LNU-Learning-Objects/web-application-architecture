# The continuous way of web application development

# The continuous way of web application development

This text will give you a hint about terms like Continuous Integration (CI), Continuous Development (CDev) and Continuous Deployment (CDep). It will try to explain the difference between these terms and also try to answer the questions what and why.

To get a clearer image of these terms we need to take a look back. Software development has been a subject for many years, long before the web and web applications (which this text is focusing on). One common project model was the waterfall model. Every part in the development was made in isolated steps. First all the requirements were collected, then the planning started, then the development and when the code was ready a integration phase begun and so on. The integration was often experienced as a game. Code that has been isolated for month should run together and hopefully everything in the application will work. Of course that wasn't the case in most projects. Since the code had grown isolated problem and bugs was implemented early in the code but the teams didn’t found them until the big integration, probably a integration with a tight time frame before a promised release. Problems that could had been solved easy become more complex and hard to fix and no one had the whole picture. A lot of stressed work is to be done and there will be a big risk that bugs find their way out to production.

Today we see more project that are using a more iterative model since we realized that software ideas change during the process. We have also realized that integration should be done continuously. We must found eventual problem and bugs as soon as possible. As you understand is what the term Continuous Integration (CI) is all about.

## A Continuous Integration workflow 

The term came from the eXtreme Programming (XP) community [ref] and has been around for a while. A team with many programmers produce different chunk of code handling different features of the application. The applications main code should live in a shared repository where developers push or merge code several times a day. This will start a integration process where the code should validates against static analyzes (like code hinting) and run tests. That will catch some of the bugs and problem early in the process and force the developers to fix this before it grows to a bigger problem.

CI does not only refers to integration of code. In the CI pipeline you should also build and test your code within the development environment. Imagine we have a team of a couple of developers writing code for a specific application.

But remember, there are no silver bullets when talking about web application development.
,

What we must know is that there will never be silver bullets in software development. The complexity of the applications, projects, teams, technology and so on will always be different. 


