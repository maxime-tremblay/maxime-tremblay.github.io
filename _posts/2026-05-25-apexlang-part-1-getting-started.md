---
layout: post
title: APEXLang - Part 1 - Getting Started
tags: [APEXLang, VS Code, SQLcl, AI, APEX26]
---

APEX 26.1 was released on May 14, 2026. Turns out "soon" was now.

With it came APEXLang, something the community had been waiting on for a while. It opens up APEX application development to AI assistants in a way that wasn't possible before, and it's going to change the way we work, or at least the way we think about working.

I've been talking to people around me who are less familiar with AI, and the questions keep coming up. How does it work? Where do I start? What does this actually change day to day? I didn't have a single good place to point them to, so I decided to build one.

This is the first post in a series where I'll be working through all of it. How everything connects, how to get set up, how to actually build things with AI assistance. I'm not going to pretend I have all the answers. I'm figuring a lot of this out as I go, and that's kind of the point.

## What Is APEXLang?

APEXLang is a file-based representation of an APEX application. Every component in your app, pages, regions, items, processes, dynamic actions, has a corresponding file or folder on your local machine. You work with those files in VS Code, and when you're ready, you push the changes back to the database.

The APEX Builder isn't going anywhere (at least for now). You can still use it. But with APEXLang, it's no longer the only place where development happens.

This matters more than it sounds at first. When your application lives as files, you get access to tools and workflows that were never possible with a browser-based editor. Version control becomes more natural, merging is now possible. Code reviews become possible. And AI assistants, the kind that work directly with files in your editor, can actually help you build things.

## Why This Changes Things

Working in the APEX Builder is fine for a lot of tasks. You know the interface, you know where everything is. But the moment you want to bring in AI assistance, do a proper diff between versions, or automate a deployment, you're working against the grain of a tool built around browser sessions, not files.

APEXLang flips that. Your application is just files. You can open them, edit them, compare them, commit them to Git, and hand them off to an AI assistant the same way you would any other code. The database and APEX are still doing the heavy lifting on the runtime side, but the development workflow is now closer to what you'd expect from any modern software project.

On top of that, because the files can be processed by AI tools, the way you write APEX applications can change. Instead of clicking through the builder to configure a report, you can describe what you want and let the AI generate the configuration. That's a big shift, and it's what most of this series is about.

## What You'll Need

Before going further, here's what you need to follow along:

- **VS Code** [link](https://code.visualstudio.com/){:target="_blank"} - the editor we'll be using throughout the series
- **SQL Developer extension for VS Code** [link](https://marketplace.visualstudio.com/items?itemName=Oracle.sql-developer){:target="_blank"} - connects VS Code to your database, lets you browse your schema, run SQL, and export or import APEXLang files. Having the latest version (26.1.2) is recommended
- **SQLcl** [link](https://www.oracle.com/database/sqldeveloper/technologies/sqlcl/){:target="_blank"} - Oracle's command-line interface; the SQL Developer extension uses it under the hood to talk to the database. Having the latest version (26.1.2) is recommended
- **ORDS 26.1.1 or later** [link](https://www.oracle.com/database/technologies/appdev/rest.html){:target="_blank"} - required by APEX 26.1
- **APEX 26.1** [link](https://www.oracle.com/apex/){:target="_blank"} - APEXLang was introduced in this version and is not available in earlier releases
- **Oracle Database 19c (with Database Release Update 19.18 or newer) at minimum** - though for the full APEX experience, Oracle AI Database 26ai is recommended; some features won't be available on older database versions

If you haven't read the [APEX 26.1 announcement](https://blogs.oracle.com/apex/announcing-oracle-apex-261){:target="_blank"} or had a look at the [what's new page](https://www.oracle.com/apex/whats-new/){:target="_blank"} yet, that's worth doing before going further.

> **Note:**  
> As of writing this post (May 15, 2026), OCI only has version 24.2 available. The 26.1 version will be slowly rolling out across regions over the next few weeks.

> **Note:**  
> If you don't have a local instance to test with, you can use the [free Oracle-hosted APEX instance](https://oracleapex.com/ords/r/apex/quick-sign-up/request-workspace){:target="_blank"} to get started. Keep in mind that since you can't connect directly to the underlying database, some features may not be available.

> **Note:**  
> As of writing this post (May 15, 2026), the [Pre-Built Developer VMs for Oracle VM VirtualBox](https://www.oracle.com/downloads/developer-vm/community-downloads.html){:target="_blank"} haven't been updated yet to include APEX 26.1. Hopefully that changes soon.


## What to Expect From This Series

This is a seven-post series. Here's what's coming:

- **Post 2: Architecture Overview** - how VS Code, SQLcl, ORDS, and the database all connect, plus a look at MCPs and what they make possible
- **Post 3: Setup and Workspace Architecture** - configuring VS Code, SQLcl, and your project structure for APEXLang development
- **Post 4: Development Workflow Overview** - the core loop of exporting, editing, and importing APEXLang files, with a comparison of vibecoding versus specs-based development
- **Post 5: Deep Dive** - a full hands-on walkthrough with video: vibecoding an app, extracting specs, rebuilding from specs, and comparing results across AI tools
{% comment %}
- **Post 5: Online AI vs. Local LLMs** - comparing online AI tools like Claude, Copilot, and ChatGPT against local models like Ollama, with notes on privacy, cost, and when to use each
- **Post 7: Setting Up Local LLMs** - a practical guide to running AI models locally with Ollama, for teams with privacy requirements or cost considerations
{% endcomment %}

More on all of this in the posts ahead!