---
title: Object-Oriented Finance Data Model
date: '2012-06-20'
description:
categories: oof
tags: [finance, objectoriented]

layout: post
---

Below is a list of the different entities in the *Object-Oriented Finance (OOF)* data model. This is an attempt to organize all of the relevant concepts in the financial universe into a coherent and consistent system. Once this clarity is achieved (and only then), our goal is to translate this model into software.

The primary tool we will use is the *Class-Responsiblity-Collaborator (CRC)* method. Each entity in our model has a "card" outline the (1) name of the entity, (2) the entity's definition and its responsibilities, and (3) the other entities that it must reference to fulfill these responsibilities.

We will start with a very fundamental concept: time.

### Class: TimeLine

Provides a single index of all time. 

#### *Responsibilities*

Is the only instance of itself (a *singleton*). Locations on the TimeLine are Instants and are denoted by a unique timestamp in the following format

    2451544.86399999

which represents 23:59:59.999 on December 31, 1999 using the *Julian Date - UTC* convention.

### Class: Instant

A single location on the TimeLine. 

#### *Responsibilities*

Can tell me its unique location, expressed in the *Julian Date - UTC* format. 

#### *Collaborators*

TimeLine

### Class: Interval

A closed interval (containing its endpoints) on the TimeLine.

#### *Responsbilities*

Can tell me its start and end points, both of which are Instants. 

#### *Collaborators*

Instant, TimeLine

### Class: Asset 

Something that is legally exchangeable with other Assets in some Venue.

#### *Responsbilities*

Can be exchanged in ownership or in possession with other Assets.

### Class: Fiat Asset

Asset created by a Sovereign Agent from nothing that can exchanged for any Asset in the Sovereign's Venue.

### Class: Fungible Asset

Agents are indifferent between individual units of a Fungible Asset. They are mutually exchangeable.

### Class: Lendable Asset

An Asset that can be leant from one Agent to another

### Class: Security

A standard Asset arranging a Transaction.

#### *Collaborators*

Transaction

### Class: Contingent Claim

A Security granting the right to engage in a Transaction.

#### *Collaborators*

Agent, Transaction

### Class: Commodity

An Asset that can be consumed. 

### Class: Venue

Gives a context for the laws and taxes that are available to Agents.

