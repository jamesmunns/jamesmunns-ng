+++
title = "Shepherding v3.1"
date = 2019-09-12
draft = false
in_search_index = true
template = "blog_post.html"
+++

For open source projects, it can be difficult to find balance between a number of factors: the free time of contributors, the desires of the communities using the project, the ability to on-ramp and mentor new contributors, and to provide necessary guidance and feedback.

The Rust Projects, and multiple sub-teams and working groups have found success in use of the [RFC Process] for making informed, high level decisions. However, the RFC process does not address the work necessary for exploratory projects before a decision is made, the work necessary to implement made decisions, or the work necessary to maintain and overhaul parts of the projects in the long run.

[RFC Process]: #

To address these needs, I'd like to propose a general concept and approach called **Shepherding**, which aims to assist maintainers of these projects with this aspect of the managing the project. By enumerating core goals and putting a name to concept, but specifically NOT mandating every aspect of implementation, I hope that this technique can be applied across many teams inside and outside of the Rust Project.

The "Shepherding 3.1" name comes from a blog post written by Niko Matsakis titled [Shepherds 3.0], which also does an excellent job describing the motivations regarding these efforts. This post instead makes a few clarifications and additions to the 3.0 post, and aims to be a "reference manual" for the concept, defining terms and important goals, rather than discussing motivations.

[Shepherds 3.0]: http://smallcultfollowing.com/babysteps/blog/2019/09/11/aic-shepherds-3-0/

<!-- more -->

## What Shepherding is, and is not

The concept of Shepherding has a few concrete aims:

1. To address the needs of volunteer driven open source projects
2. To limit the amount of work in flight at once by requiring a shepherd for all tasks
3. To provide accountability and visibility to things that are, and are not, in progress
4. To provide a structure for collaboration, including for established contributors as well as new or prospective contributors
5. To define consistent terminology, allowing members of similar teams (e.g. the Rust Language Team and the Rust Embedded Working Group) to share a common understanding of how each other operates
6. To empower maintainers by giving them tools to manage their projects and the expectations of the people using their project
7. To empower contributors by giving them documented ways to become involved with the projects

The following are specifically NOT aims of Shepherding:

* Shepherding does not aim to be a design or decision making process, at least not in the way that the [RFC Process] aims to be
* Shepherding does not aim to prescribe what SHOULD be worked on. As open source projects are largely volunteer driven, it should provide a structure for people to contribute to things that matter to them.
* Shepherding does not prescribe a strict implementation, but instead provides a framework that can be adapted to teams with different needs
* Shepherding does not aim to be a general purpose management or time tracking framework applicable to companies or non-volunteer projects

## Shepherding By Example

The following is a step-by-step guide to setting up Shepherding for a project. For a definition of the terms used here, see the [Important Concepts](#important-concepts) section below.

### Step 0: Set up your project

You need to answer the following items for your project:

1. Who are the shepherds in your team?
    * This could be all or a subset current contributors in your repository or organization
2. What is tracked for each task?
    * See below for an example template using a markdown file to maintain information about each task
3. Where are tasks tracked?
    * A folder with all tasks in your repo or a separate coordination repository is a great place to start, e.g. a `tasks/` folder in your repository, or a `tasks` repository in your organization
    * Subfolders for each of the different task states can be useful for organization, e.g. `tasks/in-progress/` or `tasks/rejected/`
4. How are tasks added, and how is the task state updated?
    * Pull or Merge Requests can be useful for this. Contributors can open PRs to suggest tasks, receive feedback on their proposal, and solicit a shepherd
    * Pull requests can also be used to update state, either changing information within the task, or moving the task from one state folder to another
5. How can potential contributors solicit a shepherd?
    * Is there a mailing list, chat room, or other venue used by shepherds?
    * Is it acceptable for potential contributors to directly mention shepherds in the PRs proposing a task?
6. Where and when is status of a task tracked?
    * Does your team have a regular meeting that can be used to discuss all open tasks?
    * How often does your team need to meet to discuss all open tasks, and what format should updates be presented in?
7. What are the task states used by your project?
    * For example, the following might be a good initial set of states:
        * Proposal - A PR is open and feedback or a mentor is needed
        * Active - Work is occuring actively on this task
        * On Hold - Work is not active currently, but is expected to resume
        * Rejected - Work is not expected to resume
        * Completed - Work as finished on this task
8. When and how does a task move from one state to another? What should happen when moving to each state

For each of these questions, you should document the answers in a publicly accessible location, such as `CONTRIBUTING.md` in your repository. This becomes a central place to point potential contributors who are interested in getting involved.

### Step 1: Proposing a Task

### Step 2: Accepting a Task

### Step 3: Status Updates

### Step 4: Completing a Task

### Step 5: Iterate

## Important Concepts

The following concepts are a core part of the Shepherding process:

### Teams

A team in the context of Shepherding is a collection of multiple contributors and maintainers working towards a common goal. In practice this could be a single open source project, a collection of related open source projects or libraries, or a subset of a larger open source project.

### Tasks

Tasks tracked by the Shepherding process are intended to be larger scale works, with a fixed "end goal", that can be achieved by a group of people, and are not blocked by outside factors outside of a project or the control of the team.

Tasks could include investigation of possible new techniques or approaches, implementation of already decided goals, or refactoring/improvements of existing parts of a project.

### Task States

Tasks are expected to have a set of defined states (as in states in a state machine), and a documented way for a task to progress between these states.

Different teams may decide on a differing set and number of states that make sense for them, but all projects should concretely document these states and how they are tracked.

### Task Listing

The Task Listing should be a single place where all current and previous tasks should be enumerated. This allows for project-wide visibility on what is currently in progress, as well as the previous tasks that have or have not been successful.

### Shepherds

Shepherds are typically members of a project team, and are expected to be responsible for overseeing and providing updates on a task while it is in progress. Shepherds are also responsible for coordinating with anyone working on a given task.

### Status Updates

Status updates are a regular check-in of the team with any shepherds actively working on a task. This update could take the form of a mailing list, chat meeting, video call, or in person meeting. These meetings should occur at a scheduled cadence (e.g. weekly, monthly), and they should be open to all contributors to the project.

These updates are intended to give the team visibility on the progress of each task, and allow discussions whether the state of any task should be updated.


