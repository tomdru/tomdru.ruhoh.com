---
title: Using the Object-Oriented Finance Object Model
date: '2012-06-28'
description:
categories: objectorientedfinance
tags: []

layout: post
---

The following demonstrates some examples of how the concepts in the OOF object model interact with one another and can be used to solve real problems in finance.

### Calculating the present and anterior value of a future payment

A Payment is the future transfer of ownership of a certain amount of some Asset. This Payment is defined by four things: the Asset involved, the amount of the Asset involved, the Payor (an Agent), and the Date we will transfer the Payment. Imagine the Asset is just our Currency, that we are considering the payment of 100 units of it, that our payor is the Sovereign (assume no credit risk), and that the payment will take place on 1/1/2017 (5 years from now).

As with any Asset, a Payment has some present value and some anterior value. An Asset's present value is the amount of Currency we would need to exchange on today's Date to receive 1 unit of the Asset on a future Date. We need to know (1) the future payment Date and (2) the Market with which we are dealing. The need for a future Date is obvious. The Market is useful because anyone who uses it can access any of the Market's DiscountFactorCurve. A DiscountFactorCurve is a function that takes as input an Interval and provides a DiscountFactor. A DiscountFactor is the present value of 1 unit of Currency received on a future Date with respect to a Reference Date.

To calculate the present value of a Payment, I can go to my Market and ask it for its DiscountFactorCurve. I can then ask the DiscountFactorCurve for its DiscountFactor for 1/1/2015, a possible transfer Date, with respect to today. I finally ask the DiscountFactor for its level and it tells me 0.98. I then multiply this value by my 100 units of Currency and conclude that the Payment's present value is 98 units.

Note that nowhere in my calculation did I use the date on which we transferred ownership of the Payment. It won't matter if we transfer ownership in 2014 or 2015, or at the actual moment of the payment. It *will*, however, matter if the transfer Date occurs after the payment Date since this doesn't make sense. The present value of the Payment for any date strictly greater than the Payment Date is zero.

The Payment's anterior value behaves differently. The anterior value for today's Date is the same as today's present value. The anterior value on the payment Date is equal to the size of the Payment, the face value. In between, the anterior value is equal to the amount of the payment times the inverse of the DiscountFactor level from today to the transfer date. After the payment Date, the anterior value is zero.
