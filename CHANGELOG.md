## 2.3.0-pre.11

enyo.Model.set() now supports the force parameter.

## 2.3.0-pre.10 (9 October 2013)

Removed macro support from bindings

Changed bindingDefaults to only apply to the bindings defined in the
description in which it lives

Changed computed and observers to use space delimited string of dependent
properties instead of array (array still supported, but deprecated)

Computed properties now send previous and current values to their observers.

enyo.ViewController.resetView removed, replaced with resetView property that
controls if the view is automatically recreated when destroyed.

Removed internal "concat" property, replaced by concat static method on kinds.
Should have no application impact unless code was extending the framework in
very deep ways.

Fixed missing "release" event for end of hold gesture, bug introduced in
2.3.0.pre.8

Fixed regression with this.inherited's handling of replacement argumments.

enyo.trim() updated to use native String.prototype.trim() when available.

Change to enyo.Model `parse` method handling, before it was confusing to
developers because it was only executed under specific circumstances (there
were reasons for this) but now it will be executed on all fetched data and all
data passed to the constructor (when call `new enyo.Model` and passing
attributes, or when it is created using `enyo.store.createRecord` or an
_enyo.Collection_ instantiates it). This does require that the method checks
to see what data is being passed in if it was relying on this method to
reformat fields or meta-properties from remote data but also creates local
records that already have the correct data format.

Change to enyo.Model `merge` strategy that now accepts instanced record(s) or
data hash(es), can merge without forcing the record to be instanced, and to
remain inline with the `parse` method change will parse any data being merged
if it is a data hash (not if it is an instanced record). This method no longer
accepts the optional second parameter.

Change to enyo.Model `add` method that no longer accepts optional third
parameter and will automatically call the model's `parse` method if it is a
data-hash (not an instanced record).

Added framework method `enyo.getPosition` that returns an immutable object with
the most recent _clientX, clientY_, _pageX, pageY_ and _screenX, screenY_ values.
As noted in the documentation, IE8 and Opera both report inconsistent values for
_screenX, screenY_ and we facade the _pageX, pageY_ values for IE8 since they are
unsupported.

The _enyo.Application_ `controllers` property has been deprecated. While current
code using it should continue to execute properly it is recommended you update your
applications to use the `components` array instead and bindings from `.app.controller.name`
should instead be `.app.$.name`. References of the `controllers` property on instances
of _enyo.Application_ are actually using the `$` property by alias. *THIS FUNCTIONALITY
WILL BE REMOVED IN THE NEXT MAJOR RELEASE AFTER 2.3.0*.

The `defaultKind` of _enyo.Application_ has been set to _enyo.Controller_.

The _enyo.Collection_ kind is now a subkind of _enyo.Component_ which means it now inherits
from the _enyo.ObserverSupport_ mixin as opposed to the special observer support in
_enyo.Model_.

The `global` property has now been moved to a property of the _enyo.Controller_ kind
and _controllers_ whose `global` flag is set to `true` will *not be destroyed even if
their `owner` is an _enyo.Application_ that is being destroyed*.

You can no longer retrieve an index from _enyo.Collection_ use the `get` method.
