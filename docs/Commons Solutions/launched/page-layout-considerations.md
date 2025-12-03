---
title: Salesforce Page Layout Considerations
nav_order: 3
parent: Launched Solutions
grandparent: Commons Solutions
---

# Salesforce Page Layout Considerations

**Page Layout Considerations**

**Contributors**
- Erica Buckingham
- Tony Carollo
- Katie Chu
- Daniel Kwolkoski
- Christopher Littlefield
- Geoffrey Tennent

**Introduction**
As the information on your record page becomes complex, you need to determine the best way to present record information for each object. Will a default Lightning Record Page layout work for you or will you need to use Dynamic Forms and Dynamic Actions? This article provides guidance and improves clarity for Salesforce admins working with Page Layouts, Lightning Record Pages, and Dynamic Forms and Actions allowing for effective and informed decision making when considering which option to use for each object.

**Considerations**

| | **Default Lightning Record Page** | **Lightning Record Page with Dynamic Forms & Actions enabled** |
|---|---|---|
| **Description** | LRP using "Record Detail" component; dynamic forms and actions **are not** enabled | LRP with dynamic forms and actions enabled |
| **Benefits** | • Simpler management of page layout assignments<br>  ◦ 1-1 when not customizing LRP | • Add fields from lookup records on the page<br>• Segment fields into tabs<br>• Conditional visibility available on<br>  ◦ Single Fields<br>  ◦ Actions<br>  ◦ Sections<br>  ◦ Components<br>  ◦ Tabs<br>• Add icons/colors to individual fields<br>• Add any related list to record page<br>• Add related lists from lookup objects |
| **Limitations** | • Related Lists must be on the classic page layout to show<br>• Conditional visibility only available on<br>  ◦ Sections<br>  ◦ Components | • Not available on Campaign, Product, and Task objects<br>• Not available for use in Experience Cloud<br>• Highlights panel disappears when scrolling<br>• Sections don't remain collapsed upon refresh<br>• "Printable View" prints Classic Page Layout<br>• Inability to preview as another user to test conditionality<br>• Field Tabbing Direction not modifiable for data entry |
| **Gotchas** | • LRP customizations are in two places (see 'Where to make edits')<br>• Page assignments are in two places:<br>  ◦ Record Detail component dictated by page layout profile assignment<br>  ◦ LRP visibility dictated by Org, App, Record Type, and Profile assignments<br>• When using Single Related List component, selected related list must be on the Classic Page Layout<br>• Updates to the LRP only works on Mobile if you enable "Dynamic Forms and Dynamic Highlights Panel on Mobile" setting in Salesforce Mobile App<br>• Lots of conditional visibility can slow down screen loading | • For inline editing (List Views and Reports), field needs to be added to Classic Page Layout<br>• "New" record screen uses Classic Page Layout (and therefore doesn't respect conditionality)<br>• Conditional visibility:<br>  ◦ Lots of conditional visibility can slow down screen loading<br>  ◦ Does not support multi-select fields<br>  ◦ Controlling field must be in the same section to work<br>• Dynamic Forms only works on Mobile if you enable "Dynamic Forms and Dynamic Highlights Panel on Mobile" setting in Salesforce Mobile App |
| **Where to make edits** | **Classic Page Layout:**<br>• Field placement<br>• Field tabbing direction<br>• Related Lists<br>• Mobile Actions, Buttons, Links<br><br>**Page Layout Assignment** | **Lightning Record Page Editor:**<br>• Tab labels and order<br>• Lightning components<br>• Single Related Lists (must be on Page Layout)<br>• Conditional Visibility<br>• Lightning Record Page Assignment<br><br>Everything controlled by the Lightning Record Page editor |

*subject to change in future Salesforce Releases

<img src="./images/PageLayouts-LRPDecisionTree.png" width="100%" alt="Page Layout Considerations Decision Tree">

Decision tree to help you decide which form of Salesforce Page layout options is right for your use case.
