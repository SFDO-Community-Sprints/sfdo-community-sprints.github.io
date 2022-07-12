--- 
title: Scratch Orgs
parent: Tooling
---

# Scratch Org

You've probably heard the term "Scratch org" thrown around in a lot of contexts, but what is it exactly? A Scratch Org is simply a temporary, personal Salesforce org independent of all other orgs. You can experiment and build whatever you want in it without fear of affecting anything else.

##  Why Use This Tool

In the Open Source Commons we strive to make a Git Hub repository the source of truth for our projects. This means that everything we build can be rebuilt by other's in their own Salesforce orgs because everything needed (code and metadata) is recorded in the GitHub repository. How do we accomplish this? Scratch orgs to the rescue! Scratch orgs are great for:

- Pushing code from your computer into a discrete Salesforce instance

- Retrieving declarative changes made in them (changing those clicks into code)

- Forcing you to rebuild because they don't last long (30 days). Remember our goal of making our projects available to be built anywhere. 


## Going Deeper

Scratch orgs sound great, right? How does one get one, though? In the Open Source Commons we create all our projects using [CumulusCI](cumulusci.md) (CCI). CCI, layered on top of the Salesforce Command Line, will spin up a Scratch org of our projects with all the code, metadata, org features, dependencies and data we need to work on the project. Open Source Commons also has a Web based tool called [Metéchō](metecho.md). Metéchō takes the sometimes intimidating command line out of the equation and allows you to build scratch orgs directly from your browser in a Web interface.
