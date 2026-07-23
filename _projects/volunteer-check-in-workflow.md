---
title: Volunteer Check-in Workflow
summary: An automated reminder system built with Power Automate and SharePoint, so volunteer check-ins stop falling through the cracks.
stack: [Power Automate, SharePoint, Outlook]
role: Solo developer
timeline: "2026"   # edit as needed
---

<!-- NOTE: This write-up is kept intentionally generic. Before adding the
organization's name, exact time thresholds, screenshots, or any internal
details, check what your confidentiality agreement allows. -->

## The problem

At a nonprofit I worked with, supervisors are responsible for regular
check-ins with their volunteers. In practice, the dates lived in people's
heads or in scattered notes. Nobody got reminded when a check-in was coming
up, and HR had no way to see which volunteers hadn't been checked in on for
a long time.

They needed something automatic enough that nothing gets forgotten, but
simple enough that busy supervisors would actually keep using it.

## What I built

The organization already had Microsoft 365, so I built the whole thing with
SharePoint and Power Automate. Nothing new to buy or install.

A single SharePoint list is the source of truth. Each row is one volunteer,
with their last completed check-in, the next scheduled one, and their
supervisor. Supervisors only ever edit two fields. The workflow handles the
rest.

Scheduled flows read the list every day and send the right email at the
right time: a reminder before a scheduled check-in, a quick "did it happen?"
confirmation after, follow-ups when things go overdue, and an escalation to
HR if a volunteer goes too long without a completed check-in. When a
supervisor confirms a check-in happened, the flow updates the dates in the
list on its own.

## Decisions I'd make again

**Two editable fields only.** If supervisors had to maintain several
columns, the data would rot fast. I narrowed their job down to keeping the
next date current and answering the emails, and automated everything else.

**Escalation as a safety net, not a punishment.** The HR notification exists
so no volunteer silently falls off the radar, and the flow records when an
escalation was sent so there's a history to look back on.

**Writing the user guide myself.** I wrote a step-by-step guide for
supervisors and HR explaining each email and what to do when it arrives. A
workflow nobody understands is a workflow nobody trusts.

## What I learned

Building the flows was the easy half. The hard half was designing for the
people receiving the emails: naming each one clearly, making the required
action obvious, and cutting every field that wasn't strictly necessary.
That's what decides whether an automation survives contact with real users.
