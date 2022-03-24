---
title: Poker
date: 2022-03-22 09:00:00 +0800
categories: [扑克]
tags: [poker]
---

## 1. 名词解释

* 策略（Strategy）
  * 在每种给定的条件下，玩家对应的采用对应的行动
  * 纯策略 vs. 混合策略：在给定的条件下，如果采用纯策略，就总是采用相同的行动；而如果采用混合策略，在给定的条件下，会采用不同的行动；
* 均衡（Equilibrium）
  * 当多个玩家达到均衡状态后，只有单个玩家改变策略不可能提升其收益
  * 但并不排除多个玩家同时改变策略后可以提升他们的收益
* 胜率（Equity）
  * 针对一手牌，或者一个确定的范围，在当所有玩家都不再下注以后，获胜的概率
  * 用来评估牌力。例如：AKo 对抗 KK 的话，有 30% 的 Equity
* 期望值（Expected Value, EV）
  * 计算期望值的时候，要考虑到未来所有玩家可能的行动
* 平衡（Indifference）
  * 如果对一个玩家来说，从几个策略中选择具体哪一个，EV 都是一样的，那么这几个策略对这个玩家来说是平衡的
  * 例如，我【下注】以后，对手玩家无论是【跟注】还是【弃牌】的 EV 都是一样的，那么我的这个【下注】对手玩家来说是【平衡】（Indifference）的

## 2. 极化范围 vs. 紧缩范围

* Polarized Ranges Consist of Strong and Weak Hands
  * 翻译：极化范围只由强牌和弱牌组成。不包含中等牌，要么「坚果」要么「空气」（nut or air）
  * 极化范围时，意味这主动下注（bet or raise）。越极化，下注额越大
* Condensed Ranges Consist of Medium-Strength Hands
  * 翻译：紧缩范围由中等牌组成
  * 紧缩范围中的牌会输给强牌，赢弱牌。所以也就做抓诈范围（bluff-catching range）
* The Clairvoyance Game：一个用来展示极化范围和紧缩范围理论的 Toy Game（简化游戏）。游戏规则如下：
  * 3 张牌 A/K/Q 发给 2 个玩家：OOP（Out of Position）和 IP（In Position）
  * OOP 拿到的牌永远是 K；IP 拿到的牌要么是 A，要么是 Q
    * IP 是「极化范围」
    * OOP 是「紧缩范围」
  * 双方在下注前先各投入 $1（antes is $1）
  * OOP 首先行动。他由 2 个选择：bet $1，或者 check
  * IP 随后行动。分 2 种情况：
    * 如果 OOP 之前的行动是 bet，IP 可以选择 call 或 fold
    * 如果 OOP 之前的行动是 check，IP 可以选择 bet 或 check
  * 每个玩家在面对对方的 Bet 时，可以选择跟注（call），或者弃牌（fold）；但不能加注（raise）
    * 如果选择 call，翻牌比大小，赢家获得池子中的所有筹码
    * 如果选择 fold，对方获得池子中的所有筹码
* Clairvoyance Game 的解决：
  * 双方的 Equity 都是 50%
  * 但如果双方达成了均衡（Equilibrium），IP 的 EV 大于 OOP 的 EV（也就是说，IP 可以赢更多的钱）
    * IP 能赢钱的原因在于他的范围是「极化范围」，而 OOP 的范围是「紧缩范围」
  * OOP 首先的行动策略（OOP 的牌永远是 K）：check
  * 当 OOP 首先的行动是 check 时，IP 的行动策略是「混合策略」。其整体的 bluff 频率为 1/4，平均 4 次下注中有 3 次是 A，1 次是 Q。也就是：
    * OOP 的牌是 A 的话，总是 bet
    * OOP 的牌是 Q 的话，摸到 3 次 Q，随机 bet 其中的 1 次
  * 当 IP 的行动是 bet 时，OOP 的行动策略是「混合策略」。其整体的跟注频率是 2/3，平均 3 次里面跟注 2 次
