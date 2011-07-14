# Wildebeest
## Migrate herds of servers

## Design assumptions
* systems of 1-100 servers
* posix

## Design constraints
* Migrations are written in ruby
* Migrations are written against a single Role
* A Host is tagged with a list of Roles
* Migrations assumes a basic rolling pattern: leave load, update, rejoin
* Migrations are ignorant of specific hosts or number of hosts
  * Instead blocks are written against roles
      * eg roles[:database].each do |server| ...
  * If actually needed, can emulate via Roles
* Hosts are identified by UUID's
* Migrations are identified by git sha1
* State of a host is the sha1 of the last migration completed
* Migrations form a strict chain with no skipping, diverging or merging
  * Tempting to allow more, but erring on the side of easily predicted behavior
* Migrations are stored in source control
* Pull from git model, not push from checkout like capistrano
* Usable for both CI and Production to give confidence
* Hosts communicate their state by setting references in git
  * Migrations can wait on some condition of other hosts by polling on git
* Can add a host to cluster by cloning a VM and changing UUID
* Can restore a host by loading backup of vm and running migration

## Open problems
* Handling coordination of divergence
  * restoring a host from an old migration state might require different waiting behavior

## Simple model

* Hosts, Roles, Migrations, Changes
* Hosts are identified by uuid
* Hosts are tagged with one or Roles
* Migrations are written to iterate over Roles
* Migrations can be one time or reusable
* Migrations can be be written against tests/specs
* Applying a migration to a cluster creates a Change
* Hosts poll on a git repo
* Hosts register their migration state as references in git