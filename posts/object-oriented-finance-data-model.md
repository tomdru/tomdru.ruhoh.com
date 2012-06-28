---
title: Object-Oriented Finance Data Model
date: '2012-06-20'
description:
categories: oof
tags: [finance, objectoriented]

layout: post
---

Below is a list of the different entities in the *Object-Oriented Finance (OOF)* data model. This is an attempt to organize all of the relevant concepts in the financial universe into a coherent and consistent system. Once this clarity is achieved (and only then), our goal is to translate this model into software.

The primary tool we will use is the *Class-Responsibility-Collaborator (CRC)* method. Each entity in our model has a "card" outline the (1) name of the entity, (2) the entity's definition and its responsibilities, and (3) the other entities that it must reference to fulfill these responsibilities.

We will start with a very fundamental concept: time.

-------------------------------------------------------------------------------

### Class: TimeLine

Provides a single index of all time in Julian dates and UTC milliseconds.

#### *Responsibilities*

Is the only instance of itself (a *singleton*). Locations on the TimeLine are Instants and are denoted by a unique timestamp in the following format

**2451544.86399999**

which represents 23:59:59.999 on December 31, 1999 using the *Julian Date - UTC* convention.

-------------------------------------------------------------------------------

### Class: Instant

A single location on the TimeLine. 

#### *Responsibilities*

Can tell me its unique location, expressed in the *Julian Date - UTC* format. 

#### *Collaborators*

TimeLine
-------------------------------------------------------------------------------

### Class: Interval

A closed interval (containing its endpoints) on the TimeLine.

#### *Responsibilities*

Can tell me its start and end points, both of which are Instants. 

#### *Collaborators*

Instant, TimeLine

-------------------------------------------------------------------------------

### Class: Asset 

Something that is legally exchangeable with other Assets in some Venue.

#### *Responsibilities*

Can be exchanged in ownership or in possession with other Assets.

-------------------------------------------------------------------------------

### Class: Fiat Asset

Asset created by a Sovereign Agent from nothing that can be exchanged for any Asset in the Sovereign Agent's Venue.

-------------------------------------------------------------------------------

### Class: Fungible Asset

Agents are indifferent between individual units of a Fungible Asset. They are mutually interchangeable.

-------------------------------------------------------------------------------

### Class: Lendable Asset

An Asset that can be leant from one Agent to another

-------------------------------------------------------------------------------

### Class: Commitment

Assets that causes some agent to be obligated to execute an agent action with the commitment owner at some future time

-------------------------------------------------------------------------------

### Class: Security

Standardized assets that serve as evidence of financial commitments

#### *Collaborators*

-------------------------------------------------------------------------------

### Class: Contingent Claim

Asset that allows owner to create a commitment between an agent and himself at some future date contingent on some event.

#### *Collaborators*

Agent, TimeLine

-------------------------------------------------------------------------------

### Class: Commodity

An Asset that can be consumed. 

-------------------------------------------------------------------------------

### Class: Venue

Gives a context for the laws and taxes

-------------------------------------------------------------------------------

### Class: Agent

#### *Responsibilities*

Agents are defined as actors that interact with each other to maximize their financial wealth. These interactions take place in a venue and are uniquely indexed on the timeline.

An agent can tell me its name, its ID, the venues it interacts in, and the assets it owns.

#### *Collaborators*

Venue, Sovereign Agent, Asset

-------------------------------------------------------------------------------

### Class: Sovereign Agent

#### *Responsibilities*

A sovereign agent makes and enforces laws upon non-sovereign agents within the sovereign agent's jurisdiction.

#### *Collaborators*

Agent, Venue
-------------------------------------------------------------------------------

### Class: Deal

Standardized “de facto” terms based on market conventions

#### *Responsibilities*

Knows its terms

#### *Collaborators*

Price Taker, Price Maker, Venue

-------------------------------------------------------------------------------

### Class: Transaction

A bilateral exchange of commitments through the following
sequence of steps

 * **Initiation** -- One agent, who we'll call the price taker queries another agent, who we'll call the price maker, to quote the terms describing the collection of transfer actions.

 * **Execution** -- The agents agree to the quoted terms based on their legal jurisdiction.

 * **Settlement** -- The agents enact the agreed upon transfer actions.

#### *Responsibilities*

Knows its price taker, price maker, execution instant, execution venue, commitment to settle, settlement date, settlement actions

#### *Collaborators*

Instant, Deal, Agent, Venue, Action?

-------------------------------------------------------------------------------

### Class: Price Taker

The agent that invites the transaction by requesting the deal level for a particular deal and then decides to act.

#### *Collaborators*

Price Maker

-------------------------------------------------------------------------------

### Class: Price Maker

The agent that quotes a deal level in response to the price taker's request and then confirms acceptance.

#### *Responsibilities*

Quoting deal levels


-------------------------------------------------------------------------------

### Class: Settlement

A transfer of possession of ownership of assets occurring between two Agents taking place in a Venue on a Settlement Date

#### *Responsibilities*

Knows its Settlement Action

#### *Collaborators*

Asset, Agent, Venue, Instant

-------------------------------------------------------------------------------

### Class: Cash Settlement
All transfers of either possession or ownership of cash occurring on the
settlement date.

#### *Responsibilities*

Knows the amount of cash, the receiving Agent, and the giving Agent

#### *Collaborators*

Fiat Asset, Agent

-------------------------------------------------------------------------------

### Class: Non-cash Settlement

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------

### Class: Cash Purchase

A transaction where upon settlement the price maker transfers ownership of an asset and the price taker transfers ownership of some quantity of cash

#### *Responsibilities*

Knows its settlement date, whether the action is a transfer of ownership / transfer of possession, who the Price Taker and Price Maker is,
#### *Collaborators*

-------------------------------------------------------------------------------

### Class: Cash Sale

The price maker transfers ownership of some amount of cash and the price taker transfers ownership of some asset

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------

### Class: Deal event

Execution or quote of a transaction expressible as a deal level

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------

### Class: Execution event

The event of transaction actually taking place

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------


### Class: Quote Event

The event of one agent publicly indicating willingness to enter a transaction at
some deal-level.

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------


### Class: Index Event

The event of an index assuming a new value

We define an index to be any scalar variable observable by all agents in the market that can influence agents’ decisions to act.

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------

### Class: Observation

An agent *records* an event by creating evidence of the event. We define *evidence* of an event to be information stored as a consequence of the event from which we can recover all information about the event. The *observer* is the agent who records the event. An *observation* is the event of an agent observing some event and creating evidence of that event.

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------

### Class: Payment

A payment is the transfer of ownership and possession of a quantity of units of asset on a specific payment date.

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------

### Class: Loan

A loan is the transfer of possession of a quantity of units of asset from Agent A to Agent B, where Agent B returns the asset to Agent A at some future date

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------

### Class:

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------

### Class:

#### *Responsibilities*

#### *Collaborators*

-------------------------------------------------------------------------------
