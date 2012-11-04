---
layout: post
title: Rant On Parallel Computing
image: languages
author: Sreejith Narayanan
authorlink: http://sreejithhere.wordpress.com
summary: A personal rant on the over emphasis placed on improving programming efficiency through over analysis of loops and the difficulty of doing parallel programming in most of popular languages
---
Before I start on the topic, I want to make it clear that I am aware of functional programming languages and they might be the answer to a lot of issues raised in this post.  However I do not have any clear idea about what they are and what they do.  Also my lack of a formal knowledge of computer science may have resulted in many factual errors in the following.

Ever since Computer Science evolved as a discipline, one of the most studied topic has been optimisation of algorithms for minimising time and resource utilisation.  One of the most know tool for this is of course the *O-notation* for identifying the order of complexity of the code.  From my observation of my colleagues implementing this in their daily work, this seems to have the primary objective of minimising CPU cycles that your code will execute.

While this is definitely helpful in writing fast executing code and any system which is well analysed is likely to perform better than an untuned system.  However the big issue that I have with this over emphasis on focussing minimising the CPU cycle is that it is a relic of a time which hardware lagged in capabilities compared to what the software was asking it.  However with the relentless onslaught of Moore's law, now we have more processing power than we have need for it.  As an example, I am using an 8 core hyper threaded machine to type these words which is like killing an ant with a hammer.

This problems is further compounded by the availability of very cheap cloud resources which allow you to get enterprise level hardware capabilities at throw-away prices.  At MQuotient, we are deploying 5-10 servers every day at a cost of around Rs. 10,000 per month on AWS.  This availability of virtually infinite computer resources have made the gains from optimising the code for CPU cycles pointless.

However this brings about another problem.  All the current paradigms are oriented towards solving a problem by running it natively in the system where it is executing.  Of course each OS and each language exposes at least 5 different ways to create threads or processes.  And there are countless RPC methods which allow you to shunt the work to other machines.  We use some of these at MQuotient, with Celery and Rabbit being the flavour of the season.  However here is my problem with all these.  

**Why does this have to be so difficult that sometimes you just want to tear your hair out!**

At work, we have spent an inordinately large time on designing systems just so that we will be able to scale.  And always we end up with the same questions.

- What code do we execute where?
- How do we ensure thread safety, prevent deadlocks and ensure that the code executes in order
- How do we control data access, both for variables and for database values?
- How do we prevent bottle necks and underutilisation of resources?
- And a million others

We are long past the time when these should have been boiler plate code abstracted away by the runtime, either natively by the language runtime or by the framework.  The programmer should be allowed to concentrate on the domain problem and not be forced to think about the messaging protocol or learn esoteric frameworks to accomplish the same.

So I propose the evolution of a language or a framework which is conceptualised and targeted from ground up for addressing massively parallel processing.  The critical thing about this language is to avoid the typical compromises that languages make.  It should be unapologetically focussed on just two things

1. Minimise programmer exposure to the multi-processing
2. Optimally utilise the distributed resources to the maximum.

The target is to reduce the programmer exposure to parallel processing architecture to zero so that he is not even aware that the program will be executing in multiple machines.  And when I am talking about optimal usage of the resources, I do not mean that in a traditional computer science optimisation.  It is rather focussed towards making sure that the three critical resources - CPU, RAM and IO are perfectly balanced so that there is no bottle neck.  This would require the following

1. Prefect load balancing so that when one of the resources is underutilised in an instance, task which are intensive in those should be prioritised in that instance
2. Seamless addition and removal of new instances as needed
3. Good localisation of codes so that the network traffic is minimised - Code should come to data and not the other way
4. Excellent garbage collection

In a follow up post, I would like to start off with the initial specs for a language which can meet these requirement.  For now, the rant comes to an end.



  
