Patches and hacks for Firefox I made, mainly for ESR.
In no particular order.

## remove-normandy.patch

A patch to remove Normandy component, to be applied to source files.

## Bug1421725_WebRequest.patch

A dirty, hacky patch to "fix" Bug 1421725, to be applied to source files.

Modifies WebRequest.jsm to run and apply changes from blocking listeners sequentially, while non-blocking listeners are run in parallel as before.

This is in accordance with what the MDN says: "... the second listener will see modifications made by the first listener ..."

## monkey_Bug1421725_WebRequest.cfg

An unholy autoconfig script to monkey patch the changes as seen in Bug1421725_WebRequest.patch.

Use with `general.config.filename`. Needs `general.config.sandbox_enabled` = `false`.

## monkey_AddonSettings.cfg

An unholy autoconfig script to monkey patch AddonSettings to always make it respect `xpinstall.signatures.required`,`extensions.langpacks.signatures.required`, and `extensions.legacy.enabled`.

Use with `general.config.filename`. Needs `general.config.sandbox_enabled` = `false`.
