---
layout: page
title: Proposal
permalink: /proposal_for_calstate/
---

The Problem
------------
Los Angeles's Planning department is in the process of a paradigm shift
from a car centric policy model to one that accommodates multiple modes
and users.  This change is detailed in the "[mobility
element](http://planning.lacity.org/Cwd/GnlPln/MobiltyElement/Text/MobilityPlan_2035.pdf)"
document.  The mobility element  affects [street
designations](http://planning.lacity.org/Cwd/GnlPln/MobiltyElement/Text/CompStManual.pdf),
an attribute of GIS mapping systems maintained by the Bureau of
Engineering and the Planning department. 
   
The BOE maintains a GIS mapping system called
[NavigateLA](http://navigatela.lacity.org/NavigateLA/) that is used
internally, by city departments and the public.  BOE data is the
authority on policy created by other city departments. For example, a
developer must receive the approval of a plan check engineer who uses
the BOE's GIS data to authorize the developer's plans. When this GIS
data is inaccurate it can be a disastrous and costly situation for the
city and the developer. 

One of the departments from which BOE receives changes in policy
affecting NavigateLA's database is the Planning Department. The Planning
Department is responsible for assigning street designations. The BOE is
responsible for enforcing the rules specified for each of these
designations.  Because it is the Planning Department that specifies the
designation information, and because these designations constantly
change, BOE employees must repeatedly enter designation updates received
from Planning into NavigateLA.

This process is especially important with the respect to the new
Mobility Element. As part of the new Mobility Element, more types of
designations will be introduced, and essentially every street segment in
the city of Los Angeles will be redesignated at a block by block level.
It is expected that with this increased specificity will come more
frequent updates to a street's designation. Thus, it is important that
our tools and processes are flexible enough to handle these more
expressive designations without putting undue load on the department's
employees.

The Planning Department, in addition to updating information for the
BOE's mapping system, maintains their own mapping application called
[ZIMAS](http://zimas.lacity.org/) which is a specialized instance of
ArcGIS that receives data from the BOE's ArcGIS database.  

Details of the process of publication between BOE and Planning are
displayed in the accompanying flowcharts.  

Diagrams
--------

### Current Process

[![Current Street Designation Change
Process](http://i.imgur.com/oehD0Xp.png)](http://i.imgur.com/oehD0Xp.png)

### Proposed Process

[![Proposed Street Designation Change
Process](http://i.imgur.com/LNxhjtg.png)](http://i.imgur.com/LNxhjtg.png)

Goals
-----
 1. Increase the speed with which changes to street designations made by
    Planning are available to the plan check engineers.
   1. Reduce the amount of time spent by the Bureau of Engineering
      inputting changes to street designations
   2. Reduce the amount of time spent by Planning preparing change
      reports to send to the Bureau of Engineering
 2. Solidify the Planning Department as the sole Source of Authority for
    street designations.
   1. Reduce the chance for errors that could occur when Planning
      manually creates change request documents and when the BOE
manually re-inputs what is intended to be the same data.
 3. Introduce a working example of how service oriented architecture
    improves the quality of the city's data while also reducing the
effort of maintaining the data. 

Requirements
------------
An internet based interface for the exchange of information between
Planning and the BOE

1. Planning
  1. A webservice that publishes their existing street designation data
2. BOE   
  1. A webservice client to retrieve data from Planning's webservice
  2. A database client to integrate this data into the BOE's NavigateLA
     nightly export process

Timeline
--------
The process of accomplishing our goals will require meeting with city
officials once a week to review progress and ask questions related to
software and human infrastructure.  During the course of this project
the scope will evolve with the participation of the city employees.

Associated Software
-------------------
ZIMAS and NavigateLA are javascript applications using ESRI's javascript
API.  The backend software for both geographic applications is ESRI's
ArcGIS server on top of Mircosoft SQL database.  Web applications run on
Microsoft server operating systems and are written using coldfusion,
javascript and html.  Because we are integrating into existing system
the choice of database and language will be decided by the existing city
convention. Prior working knowledge of SQL, javascript and HTML is
assumed. Other systems used by the city will have to be learned. 

### ESRI Javascript API

Knowledge of "[ESRI JavaScript
API](https://developers.arcgis.com/javascript/)" will be necessary to
alter any front end funcationality.  This library is compatible with
jquery. 

### Mircosoft SQL database

This project will require a working knowledge of the Mircosoft SQL
database systems.

### ESRI ArcGIS server

This project will require a working knowledge of ERI ArcGIS server that
creates and manages GIS web services, applications and data.  It will
also require a knowledge of its desktop applications that include shape
files and spatial databases.

### Coldfusion

Coldfusion is a "rapid web application development platform"  with a
associated scripting language (CFML) and tag library.  A working
knowledge of ColdFusion is required for this project. 

### Webservices

Knowledge and research about web services related to the city's software
infrastructure is required for this project including SOAP and REST
services.  
  
Existing Datasets
-----------------
https://data.lacity.org/

Acronym Table
-------------
| Acronym       | Meaning                      | 
| ------------- |:----------------------------:| 
| BOE           |Bureau of Engineering         | 
| ZIMAS         | Zone Info & Map Access System|         
| GIS           | Geographic Information System|
| CFML          | ColdFusion Markup Language   |   

Primary City Partners
---------------------
Randy Price, P.E.   Division Manager Los Angeles City of Bureau of
Engineering


Claire Bowin, AICP Senior City Planner Los Angeles Department of City
Planning


Deborah Weintraub, AIA LEED_ap Deputy City Engineer Los Angeles

Graduate Advisory Board
-----------------------
Raj S. Pamula, Ph.D., Chair, Advisor Graduate Advisor


Russell J. Abbott, Ph.D. Graduate Advisor


Chengyu Sun, Ph.D. Technical Advisor


Michael Kirk Technical Advisor/Software Project Management Expert 
