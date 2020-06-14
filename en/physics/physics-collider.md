# Collision Component

## Get The Collider Component

Cocos Creator 3D currently supports two languages ​​for development, namely `JavaScript` and `TypeScript`.

**Note: It is recommended to use `TypeScript`, because it has good syntax analysis and type hints**.

Taking the example of `BoxColliderComponent`, get the `Collider` component in `JavaScript`:

1. `this.getComponent('cc.BoxColliderComponent')`
2. `this.getComponent(cc.BoxColliderComponent)`

Get the `Collider` component in `TypeScript`:

1. The same as above `JavaScript`
2. **`this.getComponent(BoxColliderComponent)`** (**Recommended, please note that the import location is `cc`**)

**Note: If there is no smart import prompt, please check if the working directory is at the top level of the project and whether you use the newer `VSCode` editor**.

## Collider and Trigger

The `Collider` component has the `isTrigger` attribute. When `isTrigger` is `true`, it is represented as a trigger, otherwise it is a collider.

**Note: The difference between collider and trigger will be introduced in [Physics Event] (physics-event.md)**.

## The relationship between `Collider` and `RigidBody`

First of all, the `Collider` and `RigidBody` components are meant to serve physical elements, and control a part of the attributes on the physical elements respectively. This also means that to understand the relationship between them, you need to first understand how the physical elements in Cocos Creator 3D are composed.

### How Elements Are Composed

In [**Introduction to Physics**](physics.md), it is introduced that a physical element is composed of `Collider` and `RigidBody` components, which indicates that there can only be one or zero physical elements` RigidBody` component, and there can be multiple `Collider` components.

It is easy to see if there is a physical element for a single node, but if we take the node chain as a unit, it will be difficult to see which nodes and which components the physical element is composed of.

For the situation of the node chain, there are currently two ideas:

1. As long as each node has a physics component, it is an element, which means that the components of the parent and child nodes have no dependencies and require multiple shapes. Add the corresponding Collider component to the node.

2. Start searching from the own node to the parent chain node. If the `RigidBody` component is found, bind its own `Collider` component to the node, otherwise the `Collider` component on the entire chain will share a ` RigidBody` component, the node corresponding to the element is the node corresponding to the topmost `Collider` component.

These two ideas have their pros and cons:

- Idea 1 is not intuitive enough. Multiple shapes can only be added to one node. To display the shape, you need to add a child node model.
- When adjusting the parameters in Idea 1, two places need to be adjusted, namely the position information of the child node and the data information of the corresponding `Collider` component on the parent node.
- Idea 2 adds the coupling of node. When a node is updated, the corresponding dependent node needs to be updated.
- When the node chain is destroyed, more content needs to be maintained, and the node chain needs to deal with complex logic when it is repeatedly destroyed in Idea 2.

**Note: The physics of Cocos Creator 3D is currently using idea 1, which may be adjusted in the future, please pay attention to the version update announcement**.

### `attachedRigidbody` property of `Collider`

The `Collider` component has the `attachedRigidbody` property. This property can get the `RigidBody` component bound to the current `Collider` component, but please note the following points:

- When there is no `RigidBody` component in its own node, this property is returned as `null`.
-`attachedRigidbody` is a read-only property.

## PhysicsMaterial

The collision body has physics material properties. Related content is described in detail in [physics material] (physics-material.md). Here, the difference between shared and non-shared interfaces is mainly introduced.

Currently, the `Collider` component provides two properties to get and set, namely `material` and `sharedMaterial`, and their differences are as follows:

1. Setting `sharedMaterial` or `material` has the same effect. It is in a shared state before calling these interfaces. When it is found that the set and the current reference are not the same instance, obtaining a material later will not generate a new material instance. At this time, it is a non-shared state.

2. Under the premise of shared state, obtaining `material` will generate a new material instance to ensure that only the current collision body references the material, so that the modification will not affect other collision bodies, and then it will be in the non-shared state.

3. Obtaining `sharedMaterial` does not generate a new one, but directly returns a reference.

---

Continue to the [physics material](physics-material.md) documentation.