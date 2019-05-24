---
description: >-
  A subsystem that enables to manage WAMP subscriptions that are re-published to
  an external non-WAMP broker.
---

# Broker Bridge

The Bondy Broker Bridge manages a set of supervised anonymous subscribers that

A subscription can be created at runtime using the `subscribe/5', %% or at system boot time by setting the application's`config\_file' %% environment variable which should have the filename of a valid %% Broker Bridge Specification File.

