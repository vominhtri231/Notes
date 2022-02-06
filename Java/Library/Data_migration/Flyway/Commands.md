# Useful commands

## Migrate

Migrate the schema to the latest version, also create the schema history table automatically if it doesn't exist, and the schema is empty.

## Clean

Drop all objects in the configured schemas

## Info

Prints the details and status information about the migrations.

## Validate

Validate the applied migrations against the available ones to detect accidental changes.

## Undo

Undo the most recently applied versioned migration.
If `target` is specified, Flyway will undo until it hit the version below the target.  
If `group`, is active, all these undos will be executed under one transaction.

### Baseline

Introducing Flyway to existing databases.

### Repair

Repairs the schema history table