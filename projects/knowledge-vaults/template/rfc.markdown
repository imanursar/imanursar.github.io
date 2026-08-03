---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: RFC Template
nav_order: 101
parent: kv - Template
permalink: /knowledge-vaults/templates/rfc
has_toc: false
grand_parent: Knowledge Vaults
---

# Request For Comment (RFC) Guidelines

RFC
{: .badge .badge-pill .badge-primary }
template
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

## What is an RFC?
RFC is an acronym for `Request for Comments`. It is a social device use to float and polish an idea prior to implementation. It provides a basic description of a problem, proposed implementation with high (and sometimes low) level detail, and a roadmap for seeing the implementation move from idea to reality.

- The “RFC” (request for comments) process is intended to provide a consistent and controlled path for new features to enter the project.
- Adopted from Open Source Community / computer networks research comunity
- RFC just as a tool to discuss ideas/context and collect feedback about it, and not as final documentation.
- It is still actively developing this process, and it will still change as more time.

## When To Write?
- **If you have an Idea for a feature or system**, write RFC and discussed it with your peers
- **If you are on “Dev Design” phase**, write RFC for your complete design spec and plan then discussed with your team
  - Make sure your milestone is justified for RFC writings
- Discussion would happen in Slack, Face-to-Face, Docs/Trello Comments, anywhere as long as updating those RFC
- Write an RFC when you’re considering something that will be hard/important to change later or impact multi aspects.
- Anyone could write RFC and discusses it. Embrace open discussion and ideas
- Write just enough, not too details but also not too abstract.
- The idea is not to have everything sorted out and planned to the detail. Is to gather context and knowledge of what needs to be done and be better prepared when implementation starts.

## How To Discuss?
- **Where?** Discussion would happen in Slack/Call, Face-to-Face, GDocs/Trello Comments, anywhere as long as updating those RFC
- **Who you should discuss with?** Tech Lead, Engineering Lead or peers that you think will affected by your ideas/design. Ask them to read and comment your RFCs.
- **When?** During/after you write RFCs for people to “grasp” your ideas.
- **What to discuss?** Anything on RFCs, ultimately looking for other people opinions
- After RFC approved it could be then continue for implementation, write your `start date`.

## How To Comment/Approve?
- **Who should comment?** Anyone or peers that think it will affected by RFC ideas/design.
- **Who should approve?** Tech Lead or Engineering Lead that supervise affected system or handle architecture. If hesitate, ask for Lead Engineers.
- **When to approve?** After anything sorted out and you could discuss all blocker possibilities
- **When to implement?** If you are confidence enough or already discussed with approvers (you should ask them directly)
- Approval could be transferred by approvers’ will

--- 

## Version

| **update date**  | **changes summary** |
| ---------------- | ------------------- |
|                  |                     |
|                  |                     |

## Header

- Title: [Title Here]
- Expected Finish Date: [YYYY-MM-DD]
- Author: [people proposing]
- Related components: 
- External Link: [if any, clickup, notion, other docs]
- Approvers: [people expect to review]

| **Name**                      | **Yes\|NotYet** | **Approved Date** | **Remarks** |
| ----------------------------- | --------------- | ----------------- | ----------- |
| [Ahmad](mailto:ahmad.com)     | Not Yet         | <YYYY-MM-DD>      |             |
| [Anshor](mailto:ans4175.com)  | Not Yet         | <YYYY-MM-DD>      |             |
| [Amalia](mailto:amalia.com)   | Not Yet         | <YYYY-MM-DD>      |             |
| [Kun](mailto:kun.com)         | Not Yet         | <YYYY-MM-DD>      |             |
| [Ramdani](mailto:ramdani.com) | Not Yet         | <YYYY-MM-DD>      |             |

- Others Reviewer(s): [written by people who expected to comment]
- Start Date: [YYYY-MM-DD]

---

## Summary
[tldr what is the business objective to be achieved, what data exists and needs to be collected, what final form is envisioned]

## Problem & Motivation / Business Understanding
[background and why the problem, what's the current status of real conditions]

## Detailed Design
[Data lifecycle]

## Dependencies
[if there is a possibility of dependency to what system or create dependency for what system]

## Milestone/Deployment Strategy
[Proposed adoption method, research development milestones or installation at production level or during real implementation]

## Data Result
[Please fill in the production data. This can include Data Flow Diagrams, Entity and Relationship Diagrams, and/or Data Model Documentation]

## Drawbacks/Risks/Possible Failures
[if there are any possible cons or shortcomings with this design, what are they. Possible failures, etc.]

## Alternatives
[What else is there besides this proposed idea? Can you include other RFCs or links to other services or links to other articles]

## Unresolved/Future Possibilities
[listing something that is still grey and unclear, needs further research, possibly in the future]

## Discussions