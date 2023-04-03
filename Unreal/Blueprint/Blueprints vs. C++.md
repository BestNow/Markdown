# Blueprints vs. C++: How They Fit Together and Why You Should Use Both

## C++

使用 C++，您使用通用的、基于文本的编程语言编写代码。

## Blueprint

更直观，专门为更高级别的游戏编程量身定制。

通过将表示事件、控制结构和函数调用的图形节点串在一起来编写代码，并通过编辑器内对话框定义数据和接口，不必用精确的语法写出定义。



## C++与Blueprint的共同点

假设有一个自定义Actor，并且希望在游戏开始时生成另一个Actor

```c++
void ACoyote::BeginPlay()
{
	Super::BeginPlay();
	if (bSpawnAnvil)
	{
		const FVector SpawnOffset(100.0f，0.0f，1500.0f);
		const FVector SpawnLocation = GetActorTransform().TransformPosition(Spawnoffset);
		const FTransform SpawnTransform(FQuat::Identity，SpawnLocation);

		FActorSpawnParameters SpawnInfo;

		SpawnInfo.Owner = this;
        AAnvil* Anvil = Getworld()->SpawnActor<AAnvil>(AnvilClass，SpawnTransform，SpawnInfo);
        if (Anvil)
        {
            Anvil->BeginFalling();
        }
    }
}
```

​	

![image-20230324221102175](.\Image\image-20230324221102175.png)





## 什么情况下使用C++

## 什么情况下使用Blueprint