Patches and hacks for Firefox I made, mainly for ESR.
In no particular order.

## remove-normandy.patch

A patch to remove Normandy component, to be applied to source files.

## Bug1421725_WebRequest_esr60.patch

A dirty, hacky patch to "fix" Bug 1421725, to be applied to source files.

Modifies WebRequest.jsm to run and apply changes from blocking listeners sequentially, while non-blocking listeners are run in parallel as before.

## monkey_Bug1421725_WebRequest.cfg

An unholy autoconfig script to monkey patch the changes as seen in Bug1421725_WebRequest.patch.

Use with `general.config.filename`. Needs `general.config.sandbox_enabled` = `false`.
