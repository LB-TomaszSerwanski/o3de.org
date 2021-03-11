---
description: ' Use the VisArea component to manage visibility and culling in Open 3D Engine. '
title: VisArea
---

{{< preview-migrated >}}

|  |
| --- |
| This feature is in [preview](/docs/userguide/ly-glos-chap#preview) release and is subject to change\.  |

A *vis area* \(visible area\) is a shape object that helps you manage visibility and culling in a scene\. When a camera is in a visible area, the camera can see only other objects that are also in the visible area\. You can use the **VisArea** component to define indoor areas and manage overdraw\. Objects are inside a visible area only if their center is inside the area\.

You can also add a **[Portal](/docs/userguide/components/portal.md)** component to an entity to create windows between visible areas\. This helps you create beautiful areas that render efficiently\.

Visible areas are only dynamic during editing\. If you modify the **VisArea** component or move the entity that the **VisArea** component is attached to at runtime, the area that the **VisArea** component defines isn't affected\. Also, the **VisArea** component doesn't work if it's spawned as part of a dynamic slice\.

For more information, see [Working with the Event Bus \(EBus\) system](/docs/user-guide/engine/ebus/_index.md)\.

**Note**
You can't modify the **[OccluderArea](/docs/user-guide/components/occluder-area.md)**, **[Portal](/docs/userguide/components/portal.md)**, and **[VisArea](#component-vis-area)** components at runtime\.

**Topics**
+ [VisArea Component Properties](#component-vis-area-properties)
+ [Vis Area Component Examples](#component-vis-area-examples)

## VisArea Component Properties {#component-vis-area-properties}

![\[The VisArea component properties in O3DE Editor.\]](/images/user-guide/component/vis-area-component-properties.png)

The **VisArea** component has the following properties\.


****

| Name | Description |
| --- | --- |
|  **Height**  |  The height of the visible area\.  |
|  **DisplayFilled**  |  Displays the visible area as a filled volume in the O3DE Editor viewport\.   |
|  **AffectedBySun**  |  Objects in the visible area are affected by the sun\.  |
|  **ViewDistRatio**  |  A multiplier on the view distance of the visible area during editing\.  |
|  **OceanIsVisible**  |  Renders the ocean outside the visible area\.   |
|  **Edit**  |  Choose **Edit**, and the component is locked for editing\. For more information, see [Editing Components in the Viewport](/docs/userguide/edit-mode-for-components.md)\.  |

## Vis Area Component Examples {#component-vis-area-examples}

**Example 1**
The following example shows two boxes\. One box is inside the visible area, and one is outside\. From outside the visible area, the inside box isn't visible\. The **DisplayFilled** option is enabled so that the visible area appears orange\.
You can see the shadow of the box inside the visible area because the **AffectedBySun** option is enabled\.

![\[The VisArea component hides one box from another.\]](/images/user-guide/component/component-visarea.png)

**Example 2**
In the same example, the **DisplayFilled** option is disabled in the visible area\.

![\[Use the VisArea component to create a shape to display and hide objects.\]](/images/user-guide/component/component-visarea-2.png)

**Example 3**
In the following example, you can see the box inside the visible area, but you can't see the box outside the visible area\.
You can see the ocean inside the visible area because the **OceanIsVisible** option is enabled\.

![\[The VisArea component displays an ocean in the visible area.\]](/images/user-guide/component/component-visarea-1.png)

**Example : Non\-Planar Legacy Vertices**
If you're familiar with the legacy visible areas, you might be used to seeing the legacy visualization\. In the legacy system, if you raise one vertex of the visible area higher than the other vertices, the legacy visualization displays the visible area incorrectly\.
The following example is the legacy visualization for a visible area\. One vertex appears higher than the others\.

![\[Legacy non-planar visible area visualization.\]](/images/user-guide/component/component-visarea-3.png)

**Example : Planar Vertices with VisArea Component**
The following is an example of the **VisArea** component with the same vertices\.

![\[Use the VisArea component to create a shape to display and hide objects.\]](/images/shared/component-visarea-4.png)

The second example is correct because the visible area is the volume on the xy\-plane with a z\-position and a height\. This makes it faster to determine whether an object is inside the **VisArea** component\.

The position on the z\-axis is the position of the lowest point\. The height is the specified height plus the difference in height between the highest and lowest point\. This remains true even after transformations\. If you rotate a visible area on the x\- or y\-axis, you might see volumes that don't make sense\. All points after a transformation are projected onto the xy\-plane\.

When legacy visible areas are converted, O3DE corrects this behavior for you\. All points are made planar, and any difference in height between points applies to the visible area's height\.