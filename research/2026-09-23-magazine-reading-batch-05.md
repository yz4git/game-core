# Magazine Reading Batch 05 — RPG, Adventure, Mastery — 2026-09-23

## Scope

Gaming Alexandriaのアーカイブから、Family Computer Magazine創刊号、LOGiN 1986年6月号、Beep 1985年12月号を中心に読み、RPG／アドベンチャー／アクション／シューティングに共通する設計知見を抽象化した。

原文や誌面の代替物ではなく、制作へ再利用できる設計原則のみを保存する。

## Sources

- Gaming Alexandria — Family Computer Magazine Issue 1, August 1985  
  https://www.gamingalexandria.com/wp/2024/07/family-computer-magazine-famimaga-issue-1-august-1985/
- Internet Archive — same issue full text / scan
- Gaming Alexandria — LOGiN Magazine, June 1986  
  https://www.gamingalexandria.com/wp/2022/09/login-magazine-%E3%83%AD%E3%82%B0%E3%82%A4%E3%83%B3-june-1986/
- Internet Archive — same issue full text / scan
- Gaming Alexandria — Beep, December 1985  
  https://www.gamingalexandria.com/wp/2026/06/beep-1985-12-01-number-12-volume-1-issue-12/
- Internet Archive — same issue full text / scan

## 1. High-score culture externalizes mastery

初期家庭用ゲーム文化では、高得点、珍しい画面、特殊な技、攻略知識などが「人に見せる価値」を持っていた。

### Mechanism
プレイ結果がゲーム外へ持ち出されると、
- 比較
- 会話
- 挑戦
- 再挑戦
が発生する。

### Design translation
現代のゲームでは、SNSボタンそのものより先に、
**見せたくなる成果物**
を作る。

候補:
- ベストスコア
- ベストタイム
- 特殊条件クリア
- レアな到達状態
- 高難度ランク
- 特殊ビルド
- リプレイ

---

## 2. “Know more, enjoy more” is a valid progression layer

攻略知識が増えるほど同じゲームが面白くなる構造は、コンテンツ追加なしで寿命を伸ばせる。

### Good knowledge
- 敵の法則
- 得点条件
- 地形利用
- リスクの高い近道
- アイテム相互作用

### Weak knowledge
- 一度見れば終わるパスワード
- 完全ノーヒントの隠しコマンド
- 操作を不要にする正解手順

### Principle
**知識は実行を置き換えず、次の判断を良くする。**

---

## 3. One simple verb can contain many techniques

当時のレビューでは、単純な一つの行為の中に複数の技巧があること自体が魅力として語られる例がある。

### Mechanism
入力数が少なくても、
- 位置
- タイミング
- 角度
- 速度
- 前後の行動
で結果が変われば、練習が技能になる。

### Principle
**操作の種類ではなく、操作一つ当たりの技術密度を見る。**

---

## 4. Rhythm can elevate familiar mechanics

既知のシューティング骨格でも、ゲーム全体の流れやテンポが良いことが魅力として評価されていた。

### Mechanism
プレイヤーは機能一覧ではなく時間の流れとしてゲームを体験する。

### Audit
- 敵出現が詰まりすぎていないか
- ボスまでの時間が適切か
- パワーアップ後に試せる時間があるか
- 強い場面の後に呼吸があるか

---

## 5. Adventure does not have to mean “hard puzzle”

アドベンチャーゲームでも、謎解き難度ではなく、物語の当事者として体験すること自体を価値にできる。

### Principle
**ジャンル名から難易度要素を自動的に決めない。**

作品の核が
- 推理
- 探索
- 体験
- 会話
- 選択
のどれなのかを先に決める。

---

## 6. Spoiler control is part of game design

攻略記事側ですら、書くことで答えになってしまう範囲を意識していた。

### Mechanism
発見する直前までの情報は興味を高めるが、答えそのものはプレイヤーの所有感を奪う。

### Principle
**ヒントは段階化し、発見の最後の一歩をプレイヤーへ残す。**

---

## 7. External knowledge must not be mandatory unless intended

原作や外部作品を知ることで有利になるゲームは成立するが、それが必須になるとゲーム単体の自立性が弱くなる。

### Principle
- 外部知識はショートカットや追加理解にする
- 進行必須情報はゲーム内にも存在させる
- ファン向け知識はボーナスとして扱う

---

## 8. Mapping plus action can create accidental friction

探索で地図記録が重要なのに、戦闘では頻繁な両手操作を要求すると、プレイヤーは物理的に作業を切り替え続けることになる。

### Mechanism
認知負荷とは別に、操作モードの切替コストが生じる。

### Principle
**異なる遊びを混ぜるとき、相互作用だけでなく切替コストもテストする。**

---

## 9. Uniform stat growth feels shallow

複数の能力値が毎回同じように伸びても、プレイヤーが選ぶことや戦い方が変わらなければ成長の意味は弱い。

### Better progression
- 選択式の伸び
- 新しい能力
- 装備との相互作用
- 戦術の解禁
- 明確な閾値
- トレードオフ

### Principle
**成長量ではなく、成長後の意思決定差を設計する。**

---

## 10. Hidden growth ceilings reduce planning

能力の上限や成長結果が必要以上に不透明だと、プレイヤーは長期計画を立てにくい。

完全な数値公開が常に必要ではないが、
- おおよその方向
- 次の解禁条件
- 何が強くなったか
は理解できるようにする。

### Principle
**不確実性を世界の謎に使い、育成システムの不親切さに使わない。**

---

## 11. Correct software is not necessarily a good game

当時の批評には、バグ取りだけでなく「楽しめるか」を何度もテストして改良すべきだという視点が明確にある。

### Principle
QAを分ける。

1. 壊れないか
2. 分かるか
3. 楽しいか
4. 上達できるか

どれか一つで他を代替しない。

---

## 12. Novel presentation cannot rescue a shallow core

グラフィックや新しいアクション表現が優れていても、中心のRPG・戦闘・成長が浅ければ批評上の弱点として残る。

### Principle
新技術・アニメーション・高品質アートを
**コアゲームの代用品にしない。**

---

## 13. Player-responsive systems create strategy when readable

敵がプレイヤーの行動を見て戦略を変える仕組みは、相手との関係性を強める。

ただし、変化条件が読めないとランダムと同じになる。

### Principle
**適応AIには「こちらの何を見て変わったか」という手掛かりを残す。**

---

## 14. Difficulty and technique are not the same

極端に難しいだけのゲームと、簡単な基本操作から高度な技巧が生まれるゲームは別。

### Principle
上級者向けの深さを作る際、
- 敵を速くする
- ダメージを増やす
より先に、
- 精度
- 効率
- 位置取り
- 連鎖
- ルート
の技能差を作れないか検討する。

---

## Immediate applications

### Puzzle RPG
- レベル上昇で盤面判断が変わるかを見る
- MEMOは外部ノート強制を減らす方向で活用
- TALKや装備は単純な数値上昇でなくルール変化へ接続
- ヒントは段階式にする

### Parry / Fighting
- 同じパリィでもタイミング・位置・反撃選択で技術差を作る
- AIがパリィ多用へ対策するとき、その理由を読めるようにする

### Racing
- 基本ステアリング一つに、進入角・荷重・出口位置など複数の技能差を持たせる
- 高難度は単に速度を上げず、ライン選択を増やす

### Shooter
- パワーアップ取得直後に使いどころを作る
- 敵出現のリズムそのものをレビュー対象にする
- 高得点条件を通常クリアと少し違う危険行動へ結びつける
