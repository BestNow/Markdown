# Gameplay技能系统

此系统可帮助你在任何现代RPG或MOBA游戏中设计、实现及高效关联各种游戏中的技能，既包括跳跃等简单技能，也包括你喜欢的角色的复杂技能集。

**Gameplay技能** 实为继承自 `UGameplayAbility` 类的C++类或蓝图类。



<ul>
    <li>技能任务
        <ul>
            <li>技能任务衍生自抽象 UAbilityTask 类，以C++编写。</li>
            <li>其完成操作时，会基于最终结果频繁调用委托（C++中）或输出执行引脚（蓝图中）</li>
            <li>例如，需要目标的技能需进行"瞄准"任务，将调用一个委托或输出引脚确认目标，并调用另一引脚取消技能。</li>
        </ul>
    </li>
    <li>Gameplay属性
        <ul>
            <li>Gameplay属性是存储在 FGameplayAttribute 结构中的"浮点"值</li>
            <li>将对游戏或Actor产生影响</li>
            <li>通常为生命值、体力、跳跃高度、攻击速度等值</li>
        </ul>
    </li>
    <li>Gameplay效果
        <ul>
            <li>可即时或随时间改变Gameplay属性</li>
            <li>例如，施魔法时减少魔法值，激活"冲刺"技能后提升移动速度，或在治疗药物的效力周期内逐渐恢复生命值。</li>
        </ul>
    </li>
</ul>


## 如何使用

由于Gameplay技能系统是一个插件，因此你需要先启用它才能使用。只需两步即可启用它：  

<ol>
    <li>在 **编辑（Edit）** -> **插件（Plugins）** 窗口中启用Gameplay技能系统插件。</li>
    <li>要使用此系统的全部功能，添加"GameplayAbilities"、"GameplayTags"和"GameplayTasks"到项目的"(ProjectName).Build.cs"文件中的 PublicDependencyModuleNames 中。</li>
</ol>


## 技能系统组件与属性

**技能系统组件** (`UAbilitySystemComponent`) 是Actor和 **游戏玩法技能组件（Gameplay Ability System）** 之间的桥梁。

Actor需要拥有自己的技能系统组件，或可以使用其它Actor的技能系统组件，才能与游戏玩法技能系统进行互动。

### 如何使用

<ol>
    <li>执行`IAbilitySystemInterface`接口并覆写`GetAbilitySystemComponent`函数。此函数必须返回到Actor相关的技能系统组件。</li>
</ol>

在大多数情况下，Actor类会有一个变量，并且有一个`UPROPERTY`标记，其中会存储一个到技能系统组件的指向器，类似于任何Actor类型中内置的其它组件。

**如何使Actor使用其它Actor拥有的技能系统组件**

这种情况一般涉及到玩家分数或者长期存在的技能冷却计时器，因为即便是玩家的Pawn或角色被销毁并重生，或者玩家拥有一个新的Pawn或角色，这些内容也不会重置。游戏玩法技能系统便可以支持此行为；如果你需要使用它，就要编写Actor的`GetAbilitySystemComponent`函数，从而让它返回到你想要使用的技能系统组件。

#### 示例

<ol>
    <li>将你的类声明为`AActor`的子项或子类（'APawn'和'ACharacter'都是比较常见的基础类），然后将 'IAbilitySystemInterface' 加到它的标头文件定义中</li>
    class AMyActor : public AActor, public IAbilitySystemInterface
     <li>IAbilitySystemInterface中的GetAbilitySystemComponent函数是必须要覆写。</li>
    virtual UAbilitySystemComponent* GetAbilitySystemComponent() const override;
    <li>在某些情况下，尤其是Actor可以被销毁和重生时，你可能需要将技能系统组件保存在其它地方，例如保存到玩家状态。</li>
    UPROPERTY(VisibleDefaultsOnly, BlueprintReadOnly, Category = "Abilities") <br>  
	UAbilitySystemComponent* AbilitySystemComponent;
    <li>在Actor的源文件中编写`GetAbilitySystemComponent`函数。</li>
    return AbilitySystemComponent;
</ol>



## 玩法技能

**玩法技能（Gameplay Ability）** 源自`UGameplayAbility`类，定义了游戏中技能的效果、使用技能付出的代价（如有），以及何时或在何情况下可以使用等。

玩法技能可以作为异步运行的实例化对象存在，因此你可以运行专门的多阶段任务，包括角色动画、粒子和声效，乃至根据执行时的用户输入或角色交互设计分支。

玩法技能可以在整个网络中自我复制，运行在客户端或服务器计算机上（包括客户端预测支持），甚至还能同步变量和执行远程过程调用（RPC）。

玩法技能还使引擎可在游戏会话期间灵活实现游戏技能，例如提供的扩展功能可用于实现冷却和使用消耗、玩家输入、使用动画蒙太奇的动画，以及对给予Actor的技能本身做出反应。

### 授予和撤销技能

- 在Actor可以使用某项技能之前，必须向其技能系统组件授予该技能。技能系统组件的以下函数可以授予对某项技能的访问：
  - `GiveAbility`：使用 `FGameplayAbilitySpec` 指定要添加的技能，并返回 `FGameplayAbilitySpecHandle`。
  - `GiveAbilityAndActivateOnce`：使用 `FGameplayAbilitySpec` 指定要添加的技能，并返回 `FGameplayAbilitySpecHandle`。技能必须实例化，并且必须能够在服务器上运行。尝试在服务器上运行技能后，将返回 `FGameplayAbilitySpecHandle`。如果技能没有满足所需条件，或者无法执行，返回值将无效，并且技能系统组件将不会被授予该技能。
- 以下函数可以利用授予技能后返回的 `FGameplayAbilitySpecHandle`，来撤销对技能系统组件中该技能的访问。
  - `ClearAbility`: 从技能系统组件中移除指定技能。
  - `SetRemoveAbilityOnEnd`：当该技能执行完毕时，将该技能从技能系统组件中移除。如果未执行该技能，将立即移除它。如果正在执行该技能，将立即清除其输入，这样玩家就无法重新激活它或与它互动。
  - `ClearAllAbilities`：从技能系统组件中移除所有技能。此函数是唯一不需要 `FGameplayAbilitySpecHandle` 的函数。

