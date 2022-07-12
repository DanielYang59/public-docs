# Frequently Asked Questions

## Where do the material properties shown on Materials Project come from?

The Materials Project core data is all calculated in-house by the Materials Project team using a variety of simulation methods. To understand the quality of these predictions, it is crucial to read the peer-reviewed publications from the Materials Project where each property is benchmarked as much as possible against known experimental values: this will give an estimate of typical error and, importantly, any systematic error that may be present.

## Why are the lattice parameters different to what I expect?

The same crystal structure can have multiple, equivalent sets of lattice parameters depending on what crystallographic "setting" is used.

Typically, there are two sets of lattice parameters reported. Lattice parameters can be defined for the **primitive** **cell**, which is a definition of the crystal with the fewest number of atoms and therefore conenient for simulations and other uses, and the **conventional cell**, which is typically easier to visualize and more like you will see in textbooks.

If the lattice parameters are very different to what you expect, check the setting first!

Some systematic errors are also present. These will typically be an over-estimation of 1–3% for most crystals. Layered crystals will also typically have significant error in the interlayer distances since van der Waals interactions are not well-described by the simulation methods (PBE) used by Materials Project. These systematic errors will be improved as Materials Project switches to user newer simulation methods (r2SCAN). See [Calculation Details](methodology/calculation-details/) for more information.

## Why is the band gap different to what I expect?

Electronic band gaps are difficult to calculate reliably from first principles, especially using methods that scale well to hundreds of thousands of materials. The method used by the Materials Project (PBE) _systematically underestimates_ band gaps.

While it would be possible to provide higher quality calculations for a select number of materials, with more accurate band gaps, it is noted that for materials discovery purposes it is useful to have a dataset that has the same systematic error. See Electronic Structure for more information.

## Why has a value changed on Materials Project?

The Materials Project presents the data it generates in two ways:

1. As individual calculations. These are always the same, and as far as possible Materials Project tries to ensure all historical calculations remain available. Typically, only advanced users will access information about individual calculations.
2. As aggregated information. This is information generated from a combination of individual calculations. This information is what is presented on the public "material details" pages, and is what most users will access. As new, improved calculations are performed, this aggregated information can change.

The Materials Project periodically updates this aggregated information in the form of new database releases. See [Database Versions](database-versions.md) for information on the latest database releases.

{% hint style="warning" %}
If performing scientific research with Materials Project data, make sure to cite the database version from which the data was retrieved. See [How to Cite](https://materialsproject.org/about/cite) for more information.&#x20;
{% endhint %}

## What is a "task\_id" and what is a "material\_id" and how do they differ?

Every database needs a unique key which can be used to distinguish one entry from another. In the Materials Project, each unique material is given a `material_id` (also referred to in various places as mp-id, mpid, MPID). This allows a specific polymorph of a given material to be referenced. For example, wurtzite GaN is assigned the `material_id` of [`mp-804`](https://materialsproject.org/materials/mp-804), while zinc blende GaN is assigned a `material_id` of [`mp-830`](https://materialsproject.org/materials/mp-830).

### How does a "material\_id" get assigned?

The Materials Project is a computational resource. All of the information on a given _material details page_ is actually a combination of data generated from many individual calculations or "tasks". It is also important that these tasks also have unique identifiers.

When a task is added to the Materials Project database, it will get an identifier assigned with the format `mp-[0-9]` ("mp-" with numbers after it). These identifiers are assigned sequentially, so smaller numbers usually refer to older calculations. An identifier referring to an _individual calculation task_ are known as a `task_id`.

When the Materials Project database is built, a unique material will then have a collection of multiple different task\_ids associated with it. The numerically smallest `task_id` will then become the `material_id`. This ensures that, as new, additional calculations are associated with the same material, its `material_id` should not change.

### In the past, I have seen material\_ids that start with "mvc", what are these?

Some calculation tasks were associated with a search for multivalent cathode materials. These tasks were given the prefix `mvc-` instead of `mp-` and thus some materials also had the prefix `mvc-`. However, this caused confusion and this approach has been retired. Tasks with the prefix `mvc-` still exist since the `task_id` cannot change, but a `material_id` will now always start with an `mp-` prefix by convention provided that at least one task associated with that material has the `mp-` prefix.

### Do material\_ids ever change? Do task\_ids ever change?

A `task_id` will never change. It will always refer to the same, individual calculation task.

A `material_id` might change in rare instances, such as the removal of the `mvc-` prefix, although this is avoided wherever possible.

If a `material_id` _does_ change, we ensure a redirect on the website is always in place, and the new `material_id` can also be found programmatically with the API using the `get_material_id_from_task_id()` function. This way, any publications or research that reference an older `material_id` are still valid, and the relevant data can still be retrieved.