---
layout: post
title: Supporting Growth
comments: true
categories: [career, development]
tags: []
---
I love structure. As a gardener, I feel like structure helps to get the most out of chaos. Recently, I tied my sweet peas shoots to the structure I’ve provided them to climb on, so that they could wrap their tendrils around it and put more energy into growing. On a similar note, this post is about how I created a structure to allow developers and their managers to understand their progression. Feeling informed and safe allows people to better match their potential.

What was the result?

## What is a progression framework?

Over the years I’ve heard a lot of different perspectives on software development job titles and how progression should work. These have ranged from a very pure view of ‘we should all just be called engineers’, up to BCS’ highly structured [SFIAPlus framework](https://en.wikipedia.org/wiki/SFIAPlus). Repeatedly I’ve been told by people in the early stages of their career that seeing their title change is the primary way they gauge their progression.

At the later stages of your career as a software developer it may well be the case you don’t really care what your title is. You measure your progress based on your influence, reputation, and financial reward. But, in those first couple of years of being a software developer while you’re waiting to be promoted into a role where you are more independent, a change in job title can be a long way away. Surely there is a way to get earlier feedback?

## Why is a progression framework important?

Career frameworks have become much more common in software development over the last 10 years as organisations as demand has forced organisations to make sure that people have a clear progression a clear career path to reduce turnover and help people to feel like they have a future. These frameworks describe what is expected of each level of software developer and maybe linked to salary bands. Showing investment in employees careers is no longer a luxury. If software employers don’t show their commitment then employees will find someone so does.

Evidence as this is shown on [Progression.fyi](https://progression.fyi), a website where organisations share their progression frameworks. The fact large employers show these off proves that organisations are competing to attract developers by highlighting the investment they have put into supporting career progression.

In a 2017 post on the [Autotrader Engineering blog about developing your career](https://engineering.autotrader.co.uk/2017/04/10/developing-your-career.html), I described how a colleague and I facilitated the collaborative creation of a progression framework to describe Autotrader’s engineering community’s understanding of what was expected of each level of software developer. Over the years since this became a critical part of the conversation around progression, and a tool used by manager of software developers. It was tweaked to clarify expectations, and adapted to include new responsibilities around maintenance and observability as Autotrader’s infrastructure platform improved.

Progression frameworks work best when they are developed in collaboration with the people they impact. Picking one of these off the shelf and forcing it on your engineers is unlikely to go well. By collaborating you ensure that people are bought into the process and that it’s tailored for your organisation’s circumstances. It is worth keeping at a pretty general level, and focusing on behaviours rather than knowledge. This way it is likely to remain relevant for longer.

Frameworks like this help both engineer and manager to understand what is expected. They provide welcome input into conversations about progression and promotion. Structuring regular performance reviews around these expectations is like a cheat code for managers. Managers of software developers find it notoriously difficult to come up with [SMART objectives](https://en.wikipedia.org/wiki/SMART_criteria) for software developers. Having expectations expressed explicitly can make it much easier to formulate objectives.

## How I iterated our existing framework to provide early careers developers with more guidance

At Autotrader, early career software developers started with one of a few job titles: Apprentice Developer; Graduate Developer; or Early Careers Developer. They aimed to progress to a Professional Developer role.

We wanted to help developers and their managers to measure their progress in those first couple of years more effectively by sharing structure which described what our expectations would be overtime. Some early career developers and their managers were already creating spreadsheets to track which parts of the Professional Developer job description they were able to demonstrate. I felt like something more fine-grained would be more useful.

I also wanted to help people focus on learning things at the right time[^knowledge-graph]. Frequently, developers would choose to focus on learning a framework before they had shown that they were able to understand the syntax of the language they were writing in. They would want to understand web service tech technologies before they had picked up good practices around how they committed their code.

[^knowledge-graph]: I believe a well-defined knowledge graph around developing software would help engineers understand what the most valuable thing to learn is as they progress, but that is a subject for a different blog post. In the meantime, sites like <http://roadmap.sh/> are helpful.

After an initial session collaborating on a whiteboard to work out how this would look, we came up with something that resembled a timeline with a series of checkpoints. Each checkpoint would have a collection of behaviours/against it.

From here, I looked through our role description for our early careers role. _Side note_: it’s a good idea to define the expectations of entry level roles; although no one will be looking at it to define requirements for a promotion it is still useful to understand performance in the meantime. I decided to use the headings in that to organise expectations around capability and behaviour. I structured some bullet points around some of the items that were mentioned.

This formed a decent prototype which could help people to understand what I was trying to achieve. As I developed this further that I decided to store it as code using [Mermaid](https://mermaid.js.org/) in a pull request against our Engineering Handbook. This allowed me to show people what it would look like.

I wanted to get input from a decent proportion of the engineering community. I didn’t want to be constrained by how many people I could get in a room, particularly since larger groups tend to stifle discussion.

To facilitate asynchronous input into the idea and the content I decided to put a Miro board, packed with plenty of descriptive exposition so that people understood what they were looking at and what input I wanted. I ran workshops where I explained what I was trying to achieve. In these I explained that I wanted their input and asked them to make comments asynchronously on the mirror board. I find many folk like to have time to think before responding. Most attendees immediately saw the potential and there were some really valuable contributions.

This validated that the idea was sound and that most things were roughly in the right place. A really useful piece of feedback was that it’s not useful to share expected timelines along with checkpoints that we described. The intention of the checkpoints was to allow managers to be more conscious of whether more support was required, based on how they observed someone progressing.

People progress through the beginning of their coding career at very different speeds, influenced bvy their prior experience and background. The early careers team at Autotrader try to encourage _sharing_ over _comparing_. One employee comparing their progress against another employee often leads to anxiety and resentment. Along the same lines, it was felt that people would look at the expected timelines and feel demotivated if their progression is didn’t match up with them.

## Launch

I launched the new framework around August 2024, in time for our new cohorts of apprentices and graduates who would start in September/October. Managers of early careers software developers were briefed around the framework by the end of the year I had a feeling that it hadn’t become an embedded part of people’s regular catch-ups with their managers. The weekly meetings I had with managers and mentors demonstrated this. 

When I heard a couple of examples of people using spreadsheets once again to track progress that I had missed a way to support the use of this resource. I realise that I could utilise the relatively new functionality in [Slack lists](https://slack.com/intl/en-gb/help/articles/27452748828179-Use-lists-in-Slack), and particularly templates. This could give people a templated list with which they could explore the framework, record the output of discussions and describe examples of how they are demonstrating things, and generally track their progress.

As I shared a link to this template with careers managers, I felt confident that this would have the effect of the framework being used more frequently. Reflecting on this months later, I decided that my more usual approach of creating versions of resources for each early grade of developer and sharing these with managers and developer via SharePoint would have been a better approach, as I would have better visibility of how much each instance was being used.

Some really useful feedback around this time was that people were struggling to know where to find the appropriate resources. We were already asking people to use a bunch of different platforms.

1. **Performance reviews** were being tracked in an in-house SharePoint system
1. **On the job learning** for apprentices had to be recorded in two separate systems
1. **Programming language syntax** and API knowledge was being tracking via a curriculum spreadsheet
1. Progress through the **early careers check points** was now in a slack list
1. The **Professional Developer role description** was published on an internal micro-site.

Although I did as much as I could to help people locate these resources, that’s a lot of places to go to understand how things are going, and it was hard for people to navigate. Each of these systems was describing progression at a different level of abstraction.

My utopian vision around this is that it should be possible for learners to track their progress as a developer using one system. They should be able to zoom in and out between various levels. I picture this as a knowledge graph with dependencies describe this relationships between topics, and topics being decomposed at various levels of detail/abstraction. I haven’t seen anything that matches this vision yet. Conversation with my former colleague—with who I initially put the progression framework together—showed that he was having similar thoughts in how to assess team maturity in his role as a software consultant. I became interested in the [BBC’s curriculum ontology work](https://www.bbc.co.uk/ontologies/curriculum-ontology) that powers their [Bitesize resources](https://www.bbc.co.uk/bitesize). I hope to one day find or develop a platform where a more consistent view can be represented using a well adopted ontology.

What would I do differently?

I wish I had spent more time sourcing expectations from apprentice and graduates early on in this process. There’s always a difficult trade-off of how much meat you put on the bones before you show somebody a walking skeleton. People are  less likely to contribute to things which look finished. At the same time, a blank page is intimidating.

By describing the process I followed, I hope to show that there is value to doing something similar. This is a significant investment of time, but it pays off. The result is that people feel better supported and have a better a clear view of their progression.

I haven’t provided this as a directive recipe. I haven’t provided the framework. I produced this resource in the same way way I believe novel software should be developed: iteratively and collaboratively.

Shameless plug: [I’m currently available](https://www.linkedin.com/posts/markcrossfield_time-to-share-some-news-after-17-and-a-bit-activity-7326256614527614976-Uody) to help carry out a similar process within your organisation. It won’t and shouldn’t produce exactly the same result, but the outcome can be just as successful.