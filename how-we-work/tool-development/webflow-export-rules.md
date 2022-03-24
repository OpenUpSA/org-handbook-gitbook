# Webflow export rules

**Rules for Webflow exports on projects that use custom JS and external developers:**

1. Do no change existing class names (unless strictly necessary to implement a request)
2. If a class name is change, ensure that change is discussed with a developer and documented in the Gitbook.
3. When making sweeping changes to an already existing component, be sure to duplicate the original component and mark the new component with a versioned name so that any changes do not break the production site. eg. ".map-options" -> ".map-options--v2".
4. Ensure that any change is documented in the Gitbook.
