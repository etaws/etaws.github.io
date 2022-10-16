---
title: Poker
date: 2022-03-22 09:00:00 +0800
categories: [扑克]
tags: [poker]
---

## 名词解释

* 策略（Strategy）
  * 在每种给定的条件下，玩家对应的采用对应的行动
  * 纯策略 vs. 混合策略：在给定的条件下，如果采用纯策略，就总是采用相同的行动；而如果采用混合策略，在给定的条件下，会采用不同的行动；
* 均衡（Equilibrium）
  * 当多个玩家达到均衡状态后，只有单个玩家改变策略不可能提升其收益
  * 但并不排除多个玩家同时改变策略后可以提升他们的收益
* 胜率（Equity）
  * 针对一手牌，或者一个确定的范围，在当所有玩家都不再下注以后，获胜的概率
  * 用来评估牌力。例如：AKo 对抗 KK 的话，有 30% 的 Equity
* 期望值（Expected Value，EV）
  * 计算期望值的时候，要考虑到未来所有玩家可能的行动
* 平衡（Indifference）
  * 如果对一个玩家来说，从几个策略中选择具体哪一个，EV 都是一样的，那么这几个策略对这个玩家来说是平衡的
  * 例如，我【下注】以后，对手玩家无论是【跟注】还是【弃牌】的 EV 都是一样的，那么我的这个【下注】对手玩家来说是【平衡】（Indifference）的

## 极化范围 vs. 紧缩范围

* Polarized Ranges Consist of Strong and Weak Hands
  * 翻译：极化范围只由强牌和弱牌组成。不包含中等牌，要么「坚果」要么「空气」（nut or air）
  * 极化范围时，意味着主动下注（bet or raise）。越极化，下注额越大

* Condensed Ranges Consist of Medium-Strength Hands
  * 翻译：紧缩范围由中等牌组成
  * 紧缩范围中的牌会输给强牌，赢弱牌。所以也就做抓诈范围（bluff-catching range）

* The Clairvoyance Game：一个用来展示极化范围和紧缩范围理论的 Toy Game（简化游戏）。游戏规则如下：
  * 3 张牌 A/K/Q 发给 2 个玩家：OOP（Out of Position）和 IP（In Position）
  * OOP 拿到的牌永远是 K；IP 拿到的牌要么是 A，要么是 Q
    * IP 是「极化范围」
    * OOP 是「紧缩范围」
  * 双方在下注前先各投入 $1（antes is $1）
  * OOP 首先行动。他有 2 个选择：bet $1，或者 check
  * IP 随后行动。分 2 种情况：
    * 如果 OOP 之前的行动是 bet，IP 可以选择 call 或 fold
    * 如果 OOP 之前的行动是 check，IP 可以选择 bet 或 check
  * 每个玩家在面对对方的下注（bet）时，可以选择跟注（call），或者弃牌（fold）；但不能加注（raise）
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

## 相同范围间的对抗

如果不是上一节的「极化」对「紧缩」的场景，而是双方的范围相同的场景会发生什么？

我们通过 Clairvoyance Game 的 2 个变种游戏来说明。

* 「变种一」：其他方面和 Clairvoyance Game 一样，除了 2 个变化点：
  * OOP 不再只能拿到 K，而是 OOP 和 IP 都可以随机获得 A，K，Q 中的一张
  * OOP 最先一次被强制只能 check

* 「变种一」的解决：
  * 双方的 Equity 都是 50%
  * IP 拿到 K 时的策略是 check
  * IP 拿到 A 和 Q 的行动策略是「混合策略」。其整体的 bluff 频率为 1/4，平均 4 次下注中有 3 次是 A，1 次是 Q。也就是：
    * IP 的牌是 A 的话，总是 bet
    * IP 的牌是 Q 的话，摸到 3 次 Q，随机 bet 其中的 1 次

分析如下：
> 当 OOP 面对 IP 的 bet 时，OOP 的跟注范围是：{A，K}，同时其跟注频率是 2/3
> 而如果 OOP 只用 A 跟注，那么这个策略的跟注频率只有 1/2，不满足 2/3 的要求。所以 OOP 需要用一定比例的 K 来跟注
> 既然 OOP 有用 K 来跟注的概率，IP 就有用 Q 来 bluff 的空间；而 bluff 频率和 Clairvoyance Game 一致：摸到 3 次 Q，随机 bet 其中的 1 次（bet 所有的 A）

* 通过「变种一」问题的解决，也总结出一个结论：当我们考虑 Bluff 的频率时，考虑的不是对方是否有比我大的牌；而是应该考虑对方拿到 nuts 牌的概率

* 「变种一」中，当 IP bet 时，OOP 用 K call 的频率是多少？
  * 考虑这个问题时，其实是先考虑 OOP 在 {A，K} 范围上，整体 call 的频率。整体上 call 的频率是 2/3（4/6），其中拿到 A 的时候是无脑 call 的；而拿到 A 的频率是 3/6，那么需要用 K call 来填充剩余的 1/6 的频率：拿到 K 的整体频率是 1/2，那么 1/6 除以 1/2 = 1/3，也就是每拿到 3 次 K，需要 call 一次（当 OOP 面对 IP bet 的时候）
* 如何计算 IP 的整体 EV？($0+$1+$2.17)/3 = $1.06（每投入 $1，能赢 6 分钱）。细节如下：
  * 当 IP 拿到 Q 时，IP 的 EV 是 $0。IP check 时 EV 为 $0；IP bet，OOP 用均衡的策略应对，IP 的 EV 同样为 $0
  * 当 IP 拿到 K 时，IP 的 EV 是 $1。IP 总是 check，进入 showdown，50% 赢 $2，50% $0，平均 EV 为 $1
  * 当 IP 拿到 A 时，IP 的 EV 是 $2.17。IP 总是 bet，OOP 在 {K，Q} 的范围上所有的 Q 都不 call，K call 1/3，EV = 5/6\*$2 + 1/6\*$3=$2.17
* 「变种一」中，如果 IP 的 bet size 不是 $1，而是 $2（也就是 IP 从压 1 赢 3 变成了压 2 赢 4），IP 能赢更多钱么？
  * 答案是不能，IP 的盈利反而降低
  * 因为，OOP 在 {A，K} 范围上面对 bet 时，A 时 call，K 时弃牌就能保证均衡；此时，双方的 EV 都是 $0

* 「变种二」：其他方面和「变种一」相同，除了 OOP 玩家可以先做 bet
  * 这样 IP 唯一的优势就只有「位置」优势了
* 「变种二」的解决：
  * IP 的 EV 比 OOP 的 EV 高（来源于位置优势）
  * 如果 OOP 玩家 check，IP 玩家是否采用和「变种一」相同的行动策略？
    * 答案：相同；IP 依然可以针对 OOP 的 K 进行 bluff
  * OOP 拿到 K 时只会做 check，我们重点讨论 OOP 用范围 {A，Q} 对抗 IP 的范围 {A，K，Q}
  * OOP 现在可以先行动，当他拿到 A 时可以采用什么均衡策略？
    * 如果拿到 A 时 check，OOP 的盈利来源于 IP 用 Q 做 bluff
    * 如果拿到 A 时 bet，OOP 的盈利来源于 IP 用 K 做 call
    * 因此，OOP 用 A 做 check 还是 bet，要看 IP 愿意用 K 做 call，还是愿意用 Q 做 bluff
      * 上一节已经计算过了，OOP 用 A 下注的整体 EV 是 $2.17
      * 当 OOP 用 A check 时，IP 用所有的 A 下注，用所有的 K check，用 1/3 的 Q 做 bluff。这样可以计算得到 OOP 用 A check 时，OOP 整体的 EV 是：$2 * 5/6 + $3 \* 1/6 = $2.17
    * 从上面的计算可以得出结论，如果 IP 采用均衡的策略，OOP 用 A bet 和 用 A check 的 EV 也就平衡的
    * 但如果 IP 的策略不均衡，OOP 就可以从用 A bet 和用 A check 中，选择盈利更多的一种来行动

### 简单小节

* 盈利来源于让对手处在「左右为难」的处境中，让其「进退两难」。例如：Clairvoyance Game 中，利用「极化范围」向对手进行施压，让他无法做出完美的选择
* 所谓的 Poker 「智慧」就是通过 bet，把对手放到一种「被考验」的场景中，让其「进退两难」
* 从「变种二」，我们也可以看到，当拿到最强牌时，也可以把 check 和 bet 混合起来，让对手难于做出选择：是否要 bluff
* 当处于范围劣势（紧缩范围）或者位置劣势（OOP）时，损失是不可避免的，所以这个时候的目标是把损失减少到最小
* 但是当面对人类对手时，可以考虑他的行动倾向，然后根据他的行动倾向来行动
* 在「变种二」，IP 在同一把牌中，可以把他的最强牌作为 bluff-catches 和 value bet；而 OOP 玩家在一把牌中，只能二选一，把最强牌要么用作 bluff-catches，要么用作 value-bet。这个就是 IP 玩家「位置优势」的来源
  * 对「位置优势」的解释通常是「信息优势」，但从这个例子来看，IP 玩家未必只有「信息优势」

## 简单数学

* Odds：如果胜率是 33%（1/3），那么对应的 Odds 是：1:2（3 次里面，赢 1 次，输 2 次）
* Pot odds：底池里面有 7500，对手下注 2500；那么我需要投入 2500 去争取获得 12500；那么当前的 Pot odds 是：2500/12500 = 1/5（20%）
* Odds & Pot odds：如果 Pot odds 比当前牌面的 Odds 划算，那么此时下注的话，是「正 EV」的动作；否则，是「负 EV」的动作
* Implied odds：计算 Pot odds 时只考虑当前下注轮次；但由于 Poker 不止一轮下注，所以如果预计能在未来的轮次能赢得更多，可以在计算 Pot odds 时把未来能赢到的钱加进来得到：Implied odds
* Outs 数：Outs 就是在等的牌，一旦真的等到 Outs 来了以后就赢了。Outs 不止一张，需要计算当前的 Outs 数，从而计算出「成牌概率」
  * 2 & 4 法则

## 规则解析

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

### 3. Ante

Ante（底注）：在发牌之前，除了 SB 和 BB 位置要分别投入大小盲注之外，还需要每个玩家投入相同的额度的筹码到底池，也就是 Ante（底注），常见的 Ante 大小是每个 1 个小盲。

例如：小盲 100，大盲 200，Ante 25 （100/200/25）的意思就是：发牌前，SB 位下注 100，BB 位下注 200，其它每个玩家下注 25；如果有 6 位玩家，那么发牌前底池里面有：100 + 200 + 6 * 25 = 450。

一般来说，Ante 的玩法有几种变化：

* 所有玩家的 Ante 由 BB 位置的玩家来给；例如：100/200/25 级别，6位玩家的话，BB 位置除了投入 200 大盲，还需要投入 150（6 * 25 = 150）Ante，BB 位置一共要投入 350
* 所有玩家的 Ante 由 BB 位置的玩家来给，但无论玩家有几位，Ante 数额不变。例如 100/200/200 的意思是：无论多少位玩家，BB 位置需要投入 200 大盲和 200 Ante，一共要投入 400

### 4. Straddle

Straddle（抓）：在发牌前，某个玩家可以声明（自愿）下 Straddle 注，大小必须是大盲注的 2 倍。同时，在翻前，做了 Straddle 下注的玩家最后一个行动。

例如：100/200 的牌局，枪口位置的玩家进行 Straddle 下注：400；随后其他玩家几次行动，最后他在大盲注玩家行动以后再行动。
