---
title: "用Python写个文字小游戏（一）"
date: 2021-09-14T12:00:00+08:00
draft: false
---
# 用Python写个文字小游戏（一）

前段时间老王写了个群友乱斗的文字小游戏，我觉得挺有意思的，决定自己也来写一个玩玩看，顺便写一个系列，连载下去。

既然是个决斗的游戏，肯定得有”人“，那就来先写个人，取个名叫Hero好了。然后先给角色一个基本属性，大名得有一个，有生命值，然后先加上攻击力和防御力，不妨先hardcode一下：

```python
class Hero:
	  def __init__(self, name: str, hp: int = 100, attack: int = 10, defence: int = 5):
		    self.name = name
		    self.hp = hp
		    self.attack = attack
		    self.defence = defence
```

然后还要写一个游戏的主类，负责整个游戏的循环

```python
class Game:
		def demo(self):
				pass

		# Main loop
	  def run(self):
		    self.demo()
```

然后就是往demo函数里面先做一个简单能跑起来的逻辑啦。

总的来说，就是让两个小人较量一下，emmm回合制吧，有一个公式，然后双方会扣除生命值，生命值先掉到0的就失败啦。

先简单设计一个公式凑合一下：

伤害值=我方攻击力-对方防御力

$damage=max(0, ATK_{me}-DEF_{enemy})$

为了防止对方防御力比我方攻击力高的时候伤害是负数变成给对方回血，做了一丢丢保护。

然后代码就变成了这样：

```python
def fight(self, attacker: Hero, defender: Hero) -> bool:
    """
    :return: true表示决出胜负，否则游戏继续
    """
    pass

def demo(self):
    me = Hero('我')
    enemy = Hero('老板', defence=0)
    while True:
			# fight函数返回true则表示
      if self.fight(me, enemy):
        break
      if self.fight(enemy, me):
        break
```

然后就是实现fight函数就好啦，还要打印一下每回合的动作，稍微增加一点观赏性...

```python
def fight(self, attacker: Hero, defender: Hero) -> bool:
    """
    :return: true表示决出胜负，否则游戏继续
    """
    damage = max(0, attacker.attack - defender.defence)
    defender.hp -= damage
    print(f'[{attacker.name}] 对 [{defender.name}] 攻击，造成 [{damage}] 点伤害')
    if defender.hp <= 0:
        print(f'[{defender.name}] 倒地不起，[{attacker.name}] 胜利了')
    return defender.hp <= 0
```

然后加一行启动代码，就能够看到简单游戏的雏形了！

```python
if __name__ == '__main__':
    Game().run()
```

来运行一下看看

```
...
[老板] 对 [我] 攻击，造成 [5] 点伤害
[我] 对 [老板] 攻击，造成 [10] 点伤害
[老板] 倒地不起，[我] 胜利了
```

嗯哼。
