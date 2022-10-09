---
title: Poker
date: 2022-03-22 09:00:00 +0800
categories: [扑克]
tags: [poker]
---

## 一. 名词解释

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

## 二. 极化范围 vs. 紧缩范围

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
    * IP 的牌是 A 的话，总是 bet
    * IP 的牌是 Q 的话，摸到 3 次 Q，随机 bet 其中的 1 次
  * 当 IP 的行动是 bet 时，OOP 的行动策略是「混合策略」。其整体的跟注频率是 2/3，平均 3 次里面跟注 2 次

* Clairvoyance Game 的变种一。其他方面和 Clairvoyance Game 一样，除了 2 个变化点：
  * OOP 不再只能拿到 K，而是 OOP 和 IP 可以随机获得 A，K，Q 中的一张
  * OOP 最先一次只能 check

* Clairvoyance Game 变种一的解决：
  * 双方的 Equity 都是 50%
  * IP 拿到 K 时的策略是 check
  * IP 拿到 A 和 Q 的行动策略是「混合策略」。其整体的 bluff 频率为 1/4，平均 4 次下注中有 3 次是 A，1 次是 Q。也就是：
    * IP 的牌是 A 的话，总是 bet
    * IP 的牌是 Q 的话，摸到 3 次 Q，随机 bet 其中的 1 次

分析如下：

> 当 OOP 面对 IP 的 bet 时，OOP 的跟注范围是：{A, K}，同时其跟注频率是 2/3
> 而如果 OOP 只用 A 跟注，那么这个策略的跟注频率只有 1/2，不满足 2/3 的要求。所以 OOP 需要用一定比例的 K 来跟注
> 既然 OOP 有用 K 来跟注的概率，IP 就有用 Q 来 bluff 的空间；而 bluff 频率和 Clairvoyance Game 一致：摸到 3 次 Q，随机 bet 其中的 1 次（bet 所有的 A）

## 三. 简单数学

* Odds：如果胜率是 33%（1/3），那么对应的 Odds 是：1:2（3 次里面，赢 1 次，输 2 次）
* Pot odds：底池里面有 7500，对手下注 2500；那么我需要投入 2500 去争取获得 12500；那么当前的 Pot odds 是：2500/12500 = 1/5（20%）
* Odds & Pot odds：如果 Pot odds 比当前牌面的 Odds 划算，那么此时下注的话，是「正 EV」的动作；否则，是「负 EV」的动作
* Implied odds：计算 Pot odds 时只考虑当前下注轮次；但由于 Poker 不止一轮下注，所以如果预计能在未来的轮次能赢得更多，可以在计算 Pot odds 时把未来能赢到的钱加进来得到：Implied odds
* Outs 数：Outs 就是在等的牌，一旦真的等到 Outs 来了以后就赢了。Outs 不止一张，需要计算当前的 Outs 数，从而计算出「成牌概率」
  * 2 & 4 法则

## 四. 规则解析

### 1. 摊牌顺序

**摊牌顺序**：河牌圈所有人完成下注后的「摊牌顺序」（Order for revealing hands when showdown）

* Players are encouraged to show their cards promptly to avoid delaying  the game, but if there is any reluctance, they are required to show them in clockwise order, beginning with the last player who bet or raised in the last betting round, or with the player who began the last betting  round if everyone checked

* 翻译：最好是所有的 Player 都主动摊牌比大小，节约时间；但如果有人不愿意先摊牌的话，可以按顺时针顺序摊牌，而第一个摊牌的人是：在河牌圈最后一个 bet 或 raise 的 Player；但如果河牌圈所有人都 check，那么从河牌圈第一个需要行动的人开始摊牌
* 不过如果你确认你拿到的是「坚果」牌，最好是主动快速亮牌（出于礼貌），不然对手可能会不爽

### 2. 有效加注

**有效加注**:「有效加注」就是你选择加注时的最少需要投入的筹码量。其规则如下：

* 如果是本轮第一个下注的玩家，那么「有效下注」至少是 1 个大盲
* 如果本轮有其他玩家下注过了，那么「有效加注」的增量不得小于前一个有效下注的增量

例如：

> 本轮下注顺序是这样的：
> A 玩家： 2bb
> B 玩家： 5bb
> C 玩家：这个时候的「有效加注」就至少是 8bb，因为 B 玩家 的下注的增量是 3bb，所以 C 玩家也至少要增加 3bb
>
> 如果这个时候 C 玩家只剩 7bb，那么他可以做 Allin。
> 在 C 玩家 Allin 之后，其他人弃牌到 A 玩家这里，A 玩家是可以继续做 raise 的，此时，A 玩家最少需要 raise 到（7bb + 3bb）= 10bb，因为 A 玩家下注之后 B 玩家进行过有效下注；
>
> 但是如果 A 玩家选择 call，那么 B 玩家不能继续下注了，因为 B 玩家下注之后只有 C 玩家进行过一个无效的下注，此时，B 玩家要么 call，要么 fold；
