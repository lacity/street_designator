---
layout: page
title: Thesis Proposal
permalink: /proposal_for_lacity/
---

<div class="site-nav">
  <h4>Contents</h4>
  <ul>
    <li>
      <a href="#goals">Goals</a>
    </li>
    <li>
      <a href="#background">Background</a>
    </li>
    <li>
      <a href="#proposal">Proposal</a>
    </li>
    <li>
      <a href="#deliverables">Deliverables</a>
    </li>
    <li>
      <a href="#timeline">Timeline</a>
    </li>
    <li>
      <a href="#outstanding-questions">Outstanding Questions</a>
    </li>
  </ul>
</div>

We intend to automate the exchange of street designation information
from the Planning Department, who specifies these designations, to the
Bureau of Engineering, who enforces these designations.

<br />
<br />

Goals (Why this is good for the city)
--------------------------------------
<a name="#goals"></a>
This will have three primary benefits.

 1. [Less time](#speed-goal) before changes to street designations
    are available to Plan Check Engineers.
    1. Reduce the amount of time spent by the Bureau of Engineering
       inputting changes to street designations
    2. Reduce the amount of time spent by Planning preparing change
       reports to send to the Bureau of Engineering
 2. [Reduce the chance for errors](#reduce-errors-goal) that could occur when Planning manually
    creates change request documents and when the BOE manually re-inputs
    what is intended to be the same data.
 3. [Support Mayor Garcetti's Open Data Initiative](#open-data-goal).

Background
----------
<a name="background"></a>

NavigateLA is a BOE Geographical Information System (GIS) used by Plan Check engineers,
to determine the designation of a particular street and assess whether
construction plans are compliant with city code.  Because it is the Planning Department
that specifies the designation information, and because these designations change 
over time, BOE employees must repeatedly enter these designation updates into their own
database in order for them to appear in NavigateLA.

As part of the new Mobility Element, new designations
are being introduced, and essentially every street segment in the city
of Los Angeles is being redesignated. The intention of having a more
expressive designation vocabulary is to more effectively meet the
nuanced needs of the diverse neighborhoods of Los Angeles. It is
expected that with this increased specificity will come more frequent
updates to a street's designation. Thus, it is important that our tools
and processes are flexible enough to handle these more expressive
designations without putting undue load on the departments employees.

Current Process (How things work now)
-------------------------------------
City Council typically makes several dozen changes to street 
designations every year, but how do these changes get from
City Council to appearing in NavigateLA?

[![Current Street Designation Change Process](http://i.imgur.com/oehD0Xp.png)](http://i.imgur.com/oehD0Xp.png)

From City Council, the authority goes to Planning, to specify the designation
of each street segment. As part of this process
planners use ArcGIS desktop software to enter the designation changes
into their own GIS. There is a public facing server for this system,
[ZIMAS](http://zimas.lacity.org). Planning notifies the BOE of these
changes via email, including a rendered map of the changes, prepared by
a planner also using ArcGIS. Sometimes Planning also includes a summary
of the changes as a spreadsheet.

Once the BOE receives this request, an engineer interprets the map and
spreadsheet into a series of edits of their own database. Nightly,
this data is extracted, transformed, and loaded into the database that
powers NavigateLA, ready for Plan Check Engineers and the public at
large to use.

Proposed Process (How we'd like things to work)
-----------------------------------------------
<a name="proposal"></a>

Instead of emailing change requests, Planning publishes their existing
street designation data through their existing ZIMAS ArcGIS Server 
and the BOE integrates this data into their nightly automated 
NavigateLA export process.

[![Proposed Street Designation Change Process](http://i.imgur.com/LNxhjtg.png)](http://i.imgur.com/LNxhjtg.png)

Deliverables (How we get there)
-------------------------------
<a name="deliverables"></a>

### Planning

The first component of our project is the Street Designations
Webservice. A webservice is a way for one system to publish data to be
used by another system over a network. The Planning department is
already using [webservices to power ZIMAS](http://zimas.lacity.org/ArcGIS/rest/services).
It makes sense to implement the new Street Designations Web Service as
just another ArcGis web service on top of ZIMAS.

### BOE

To minimize disruption, rather than build a completely new system, we
will amend the existing nightly BOE export process to pull data from the
new Street Designations Web Service, and perform any necessary
processing to get the proper data into NavigateLA.

Benefits (How this addresses the Goals)
---------------------------------------

### Speed (Less work means less time)
<a name="speed-goal"></a>

By automating the import process, Planning no longer has to take the
time to separately prepare a report for the BOE, and the BOE no longer
has to separately allocate an Engineer to input this data. Planning can
reliably expect that after publishing their data, the next day they
can see these changes online and at the Plan Check Counters.

### Reduce Errors
<a name="reduce-errors-goal"></a>

Planning is the source of authority for what designation a street has.
That means whatever designation Planning says a street is - *it is*. By
automatically populating NavigateLA with data that Planning enters we
remove the potential for a class of errors and ambiguity that comes with
humans translating change request documents.

### Garcetti's Open Data Initiative
<a name="open-data-goal"></a>

Excerpted from [the Mayors website](http://www.lamayor.org/garcetti_directs_city_departments_to_collect_data_for_open_data_initiative)

    [Open Data]...promotes a culture of data sharing and cooperation among City
    departments.

    Each City department (...) make efforts to update its public data on a
    regular basis (preferably automatically) and strive to improve
    transparency, participation, and collaboration.

The ZIMAS webservice is already public. Adding street designation data
would add to the amount of useful data being made public, and thus
clearly furthers the Mayor's Open Data agenda.


Timeline
--------
<a name="timeline"></a>

The first thing we need to do is evaluate the GIS systems for both
Planning and BOE. The existing setups will greatly inform the specific
approach of our remaining work. This will require having access to both
department's GIS databases.

The Planning departments Street Designation Webservice is the first
major component that needs to be delivered. This will require working
with the ZIMAS maintainers in Planning.

Once the Webservice is up, we can ammend the BOE's nightly NavigateLA
export process to get its street designation info from this service.
As part of this work, we'll need to set up a development environment.
Ideally we would have access to a complete setup, separate from, but
identical to the production system. At minimum, we will need access to
the source code for the automated export system, and occasional support
from the maintainers of the export process software.

Outstanding Questions
---------------------
<a name="outstanding-questions"></a>

#### How do we relate Planning's street designations to BOE's streets?

We must be able to relate the street designations from the webservice to
their corresponding street segments in the BOE GIS. There are several
different ways to accomplish this, but which is the easiest will require
some investigation of the existing schema in the GIS systems of
Planning and the BOE.

### BOE

#### How do we develop, test, and roll back our changes to the BOE nightly export?

How does the BOE currently make changes to their nightly export process?
e.g. Do you have test servers and test databases to develop against?

We don't anticipate any major problems, but part of responsible
engineering is to reasonably mitigate any foreseeable problems - how
would we return the system to it's current process?

What is the backup strategy for the affected BOE databases? How does our
work affect the BOE's ability to recover their system in the event of
failure?

Graduate Advisory Board
-----------------------
Raj S. Pamula, Ph.D., Chair, Advisor Graduate Advisor


Russell J. Abbott, Ph.D. Graduate Advisor


Chengyu Sun, Ph.D. Technical Advisor


Michael Kirk Technical Advisor/Software Project Management Expert 

Primary City Partners
---------------------
Randy Price, P.E.   Division Manager Los Angeles City of Bureau of
Engineering


Claire Bowin, AICP Senior City Planner Los Angeles Department of City
Planning


Deborah Weintraub, AIA LEED_ap Deputy City Engineer Los Angeles