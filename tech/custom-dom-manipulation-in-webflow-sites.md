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

## In-place components

In-place components are ideal for

* Page menu, hero, header, footer
* Sections that don't really change frequently or where there is no demand for maintaining them using a CMS because there are other system changes necessary to change them

In the example below, the Cash Balance and Cash Coverage sections are two instances of a Section component.

![Example in-place components before javascript populates the page with data](../.gitbook/assets/screenshot_2020-11-20_15-24-02.png)

![Example in-page components after Javascript has populated the data dynamically](../.gitbook/assets/screenshot_2020-11-20_15-29-15.png)

## Cloned components

