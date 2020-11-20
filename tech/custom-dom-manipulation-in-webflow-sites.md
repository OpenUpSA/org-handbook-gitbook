---
description: Overview of the approach and best practices
---

# Custom DOM manipulation in Webflow sites

We often build the CSS, markup and some interactivity using Webflow. We then insert custom javascript - usually to show data from an API by manipulating the DOM and injecting the data.

This approach works for sites hosted by Webflow, as well as webflow sites exported as Zip files then hosted elsewhere. When using exported sites, we generally prefer unpacking the site using [import-webflow-export](https://www.npmjs.com/package/import-webflow-export).

We refer to "components" as units of markup that can be reused. Components could be used [in-place](custom-dom-manipulation-in-webflow-sites.md#in-place-components), or included in the page in a hidden `div` as components in a "component library" and [cloned](custom-dom-manipulation-in-webflow-sites.md#cloned-components) as many times as needed.

By building components as [Webflow Symbols](https://university.webflow.com/lesson/symbols), we can update the design of the component across the site by editing it in just one place.

### General best practices

* It must be possible to select \(the DOM element of\) a component uniquely using javascript **without resorting to selecting the n-th item of a number of matches.**
* Charts should be as wide as their container and as long as is appropriate by design or configuration, possibly dynamic in height to accommodate wrapping text or other features. Chart containers should usually allow their hight to be determined by their content.

## In-place components

In-place components are ideal for

* Page menu, hero, header, footer
* Sections that don't really change frequently or where there is no demand for maintaining them using a CMS because there are other system changes necessary to change them

In the example below:

* the Cash Balance and Cash Coverage sections are two instances of a Section component.
* The blocks showing "Calculating..." actually gets replaced by a cloned component depending on whether the rating is good or bad - but the data-driven differences could be represented by changing classes in that element in-place as well.
* The header and in-page nav are also in-place components
* The search box has javascript events attached by custom javascript to handle search interaction
* The social sharing and export buttons on the top right have javascript events attached by custom javascript as well
* The chart is inserted by providing a reference to the chart container to the chart library, where the chart renders itself as wide as the container allows, and as long as the chart is designed or configured to be, possibly depending on its width.

![Example in-place components before javascript populates the page with data](../.gitbook/assets/screenshot_2020-11-20_15-24-02.png)

![Example in-page components after Javascript has populated the data dynamically](../.gitbook/assets/screenshot_2020-11-20_15-29-15.png)

### Best practices

* Use an ID to uniquely identify each instance of a component - e.g. `#cash-coverage` and `#cash-balance` above
* Don't use an ID to identify the components or elements inside a component identified by an ID - e.g. the chart container above has the class `chart-container`
  * All chart containers can be selected using `.chart-container`
  * A specific chart container can be selected using `#cash-coverage .chart-container` or as a child of a reference you already have to the ID-identified element `$("#cash-coverage").find(".chart-container")`
  * Using an ID to identify all these nested elements would result in an unnecessary maintenance burden and a good chance of duplicating IDs.

## Cloned components

