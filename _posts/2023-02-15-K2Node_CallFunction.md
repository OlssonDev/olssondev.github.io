---
layout: post
title: Make UFUNCTIONs fancier, and fast with K2Node_CallFunction
---

{: .box-note}
**Note:** If you're new to K2Nodes, I'd suggest you check out my post: [Introduction to K2Node](https://olssondev.github.io/2023-02-13-K2Nodes/).

Let's say you have a UFUNCTION you want to improve the UX or make fancier in some way but don't have the time or energy to set up a K2Node from scratch.

That's where **K2Node_CallFunction** comes in and saves the day with minimal setup!

## Create the base class

Let's make a base node for all our UK2Node_CallFunction so we don't have to add the boilerplate code for each new node.

```javascript
//.h
UCLASS()
class UK2Node_MyBaseNode : public UK2Node_CallFunction
{
	GENERATED_BODY()

	public:

	//UK2Node interface implementation
	virtual void GetMenuActions(FBlueprintActionDatabaseRegistrar& ActionRegistrar) const override;
	//End of implementation
};

//.cpp
void UK2Node_MyBaseNode::GetMenuActions(FBlueprintActionDatabaseRegistrar& ActionRegistrar) const
{
	Super::GetMenuActions(ActionRegistrar);
	UClass* Action = GetClass();
	if (ActionRegistrar.IsOpenForRegistration(Action))
	{
		UBlueprintNodeSpawner* Spawner = UBlueprintNodeSpawner::Create(GetClass());
		check(Spawner != nullptr);
		ActionRegistrar.AddBlueprintAction(Action, Spawner);
	}
}
``` 

**In progress...**