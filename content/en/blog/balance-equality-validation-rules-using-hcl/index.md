---
title: "Creating balance equality validation rules using hierarical codelists in FMR"
description: "FMR's Validation Schemes allow data managers to define balance equality validation rules. In this article we look at how Hierarchical Codelists can be used to automatically define such rules."
image: "images/posts/dataquality.png"
categories: ["FMR"]
tags: ["FMR","Validation","Hierarchies"]
date: 2022-07-22T22:22:00+08:00
author: "BIS"
type: "post"
---

Balance equalities are a useful addition to the data quality toolbox for checking arithmetic consistency between data points, often to ensure financial observations are in balance.

In FMR they are defined as structural metadata using a non SDMX standard artefact called **Validation Schemes**. 

When designing a Validation Scheme, one option is to define explicit arithmetic expressions on specific variables in a dataset. However hierarchical codelists can also be used for checking aggregate consistency within datasets.

## Checking aggregate consistency using custom expressions

Aggregate balance equalities can be defined using **custom expressions** on each dimension of a Dataflow for the purpose of checking the consistency of reported aggregates with lower-level observations. They're typically of the form:

Dimension <code>REF_AREA</code> (reference area)

````[EUR] = [DE]+[FR]+[ES]+[IT]````

The expression states that observations for <code>REF_AREA=EUR</code> must be the sum of observations for <code>DE</code>, <code>FR</code>, <code>ES</code> and <code>IT</code>.

{{< figure src="example_series.png" width="70%" caption="Example dataset of five series">}}

Expressions can use the four basic arithmetic operators: + - * /, plus parentheses (). And in addition to the form above, the following is also valid:

````0 = [EUR] – ([DE]+[FR]+[ES]+[IT])````  ... where 0 can be any constant.

Custom expressions are a good solution where the number of consistency checks required is small. For more complex scenarios involving aggregation consistency, there is another other option.

## Defining aggregate calculations using Hierarchical Codelists

In SDMX, **Hierarchical Codelists** can be used to define how aggregates should be calculated. 

It's worth noting here that the information model for Hierarchical Codelists changed in SDMX 3.0:
- the name of the structure changed from Hierarchical Codelist in SDMX 2.1 to **Hierarchy** in SDMX 3.0
- the addition of the **Hierarchy Association** structure allows hierarchies to be explicitly linked to other artefacts - in SDMX 2.1 the only way to achieve this was using Annotations 

{{< figure src="sdmx30_im_hierarchy.png" width="70%" caption="Hierarchical Codelist from SDMX 2.1 is now Hierarchy in the SDMX 3.0 information model">}}

We can achieve the same result as our example custom expression by creating a Hierarchy of the relevant codes in the <code>CL_REF_AREA</code> Codelist which defines the enumerated representation for the  <code>REF_AREA</code> dimension:
```
EUR
 |- DE
 |- FR
 |- ES
 |- IT
```

The approach starts to deliver greater benefits when aggregation hierarchies are deep and complex - maintenance of a single Hierarchy being simpler than multiple individual custom expressions.

The limitation with this approach is that the aggregation function is always assumed to be **sum**. Use custom expressions if more complex calculations are required, for example:

````[EUR] = (([UK]+[DE]+[FR]) - (([ES]+[IT]+[LUX]*10) / 2) )````

Remember also that Hierarchies are distinct from any simple parent-child relationships that may be defined as part of the Codelist. Indeed there can be any number of different Hierarchies should that need arise and a code can appear multiple times in a Hierarchy. Hierarchies can also reference codes from different Codelists but, for this use case, stick to a single Codelist.

## In practice using FMR 11

### 1. Define a Hierarchy of the relevant codes
In the FMR web user interface:
1. As an administrator or user with the appropriate Agency privileges choose **Items > Hierarchies** from the left-hand menu bar.
2. Using the 'cogs' structure maintenance menu, choose **Create New Hierarchy**
3. Wizard Step 1: Enter the basic details for the new Hierarch artefact: Id, Agency, Name, Version and Description.
4. Wizard Step 2: Use the **Add** button to add the Codelist (e.g. CL_REF_AREA)
5. Wizard Step 3: Use the **Add Root Codes** button to add those codes that sit at the very top of the hierarchy. Select a code and use the **Add Child Codes** button to add subordinate codes. The Hierarchy can be arbitrarily deep.
6. Choose the **Finish** button to save the Hierarchy.

Wizard Step 4 optionally allows the hierarchy levels to be explicitly named but this is not necessary for the validation use case. 

{{< figure src="hierarchy_example.png" width="70%">}}


### 2. Create a Validation Scheme referencing the Hierarchy
In the FMR web user interface:
1. As an administrator or user with the appropriate Agency privileges choose **Data > Validation Schemes** from the left-hand menu bar.
2. Using the 'cogs' structure maintenance menu, choose **Create New Validation Scheme**
3. Wizard Step 1: Enter the basic details for the new Hierarch artefact: Id, Agency, Name, Version and Description.
4. Wizard Step 2: Choose the Dataflow to which the validation rules will be applied.
5. Wizard Step 3: CSV Import provides a quick way enter custom expressions and can be skipped.
6. Wizard Step 4: The **Expression Builder** is where the actual rules are defined. Start by selecting the Dimension - this must use the same Codelist as the Hierarchy was defined for.
Choose **New Rule** and under **Rule Type** choose 'Aggregate Using Hierarchy'. This option will be disabled if there's no Hierarchy for the dimension's Codelist. The Hierarchy created earlier should appear, so choose that from the list. A summary of the Hierarchy will be shown for information purposes. Choose **Add Rule** will add the Hierarchy to the Validation Scheme as a rule on the selected dimension.
7. Choose **Finish** to save the Validation Scheme.

{{< figure src="hierarchy_rule.png" width="70%">}}

### 3. Test the validation rules
The new balance equality validation rule will be automatically applied whenever data is loaded for the Dataflow using the Data > Convert Data UI option, or through the REST API [data validation and transformation web service](https://fmrwiki.sdmxcloud.org/Asynchronous_Data_Validation_and_Transformation_Web_Service).

In the UI, validation results are reported under the **Valid Calculations** category.

{{< figure src="data_load.png" width="40%">}}

## Summary
FMR's Validation Schemes allow the definition of data quality rules to check consistency between observation values. 

Custom Expressions provide the flexibility of targeted rules and arithmetic expressions including addition, subtraction, multiplication and division.

However, for checking consistency between aggregation levels where the sum of lower levels should equal the values at higher levels, Hierarchies (Hierarchical Codelists in SDMX 2.1) could be the answer particularly where there are many levels. In these cases, a single Hierarchy replaces many discrete Custom Expressions reducing the creation and maintenance burden.

## References
Fusion Metadata Registry: {{% link "download/fmr" %}}download FMR 11{{% /link %}}\
Fusion Metadata Registry: {{% link "containers/fmr-docker-mysql" %}}FMR 11 Docker image{{% /link %}}