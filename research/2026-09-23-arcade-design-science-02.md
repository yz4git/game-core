# Arcade Design Science 02 — 2026-09-23

## Scope

1982年前後のコインオペレーション業界誌を読み、プレイヤー行動・難易度・報酬・情報提示・運営側の調整という観点から、現代ゲームにも使える原則へ抽象化した。

## Sources

- Gaming Alexandria — Play Meter, Volume 8, Number 14, July 15 1982  
  https://www.gamingalexandria.com/wp/2020/09/play-meter-volume-8-number-14-july-15th-1982/
- Internet Archive — 同号のOCR／スキャン公開ページ  
  https://archive.org/details/play-meter-volume-8-number-14-july-15th-1982-600dpi/

## Observation A — Game design was already being treated as measurable

業界側では、単なる制作者の勘ではなく、ゲームごとの収益推移や稼働寿命を比較し、遊ばれる理由を分解しようとする考え方が存在していた。

### Mechanism

「面白い／面白くない」を一語で扱わず、
- どの場面で継続するか
- 何を理解すると上達するか
- どのような報酬が再挑戦を促すか
へ分解すると、改善可能な変数になる。

### Generalized principle

**ゲームデザインは感覚で始めてもよいが、改善は観察可能な仮説へ変換する。**

### Transfer

現代のWebゲームなら、収益ではなく次を記録するだけでも有効。

- 初回死亡地点
- 初回クリアまでの試行数
- よく使う行動
- 使われない行動
- 離脱地点
- 再挑戦率
- 強い戦法への偏り

---

## Observation B — Prediction itself can be pleasurable

敵や対象の現在位置だけに反応するのではなく、未来位置や交差タイミングを予測するタイプの遊びが重要視されていた。

### Mechanism

予測が成立するには、ゲーム世界に一定の法則が必要。

プレイヤーがその法則を学ぶほど、
「反応できた」から「読めた」へ上達感が変化する。

### Generalized principle

**反射神経だけでなく、未来を読めるゲームにする。**

### Transfer

- Shooter: 敵の進路・弾道を読む
- Racing: コーナー出口とライバルのラインを読む
- Fighting: 次の間合いと攻撃タイミングを読む
- Puzzle: 数手後の盤面を読む
- Stealth: 巡回経路を読む

---

## Observation C — Reward does not have to be currency

当時の分析では、成功後の音、色変化、短い演出、緊張からの一時的な解放も報酬として扱われていた。

### Mechanism

小さな成功確認が頻繁に返ると、
「何をしたから成功したか」が学習しやすい。

### Generalized principle

**報酬をアイテムや数値だけで設計しない。**

報酬候補:
- 音
- 一瞬の画面変化
- 主導権
- 敵の怯み
- 安全時間
- 新しい視界
- ルート解放
- コンボ継続
- 短い演出

---

## Observation D — Breath after mastery is part of reward

高密度なアクションの直後に、短い休息や演出を挟むこと自体が達成報酬として機能するという考え方が見られた。

### Mechanism

緊張が連続すると高揚が基準化される。
短い低密度区間があることで、前の成功を認識し、次の緊張が強く感じられる。

### Generalized principle

**大きな成功の直後には、次の戦闘ではなく「成功を味わう時間」を置く。**

---

## Observation E — Visual language guides priority

色、点滅、速度、形、音は装飾だけではなく、複数脅威の中から「何を先に処理するか」を伝える情報として扱える。

### Mechanism

視覚・聴覚に一貫した文法があると、説明文なしでも優先順位を理解できる。

### Generalized principle

**危険度をUIだけで表示せず、ゲーム世界そのものに符号化する。**

### Caution

上級者向けに文法を裏切ることは可能だが、先に通常ルールを十分学ばせる必要がある。

---

## Observation F — Randomness and structure are different

当時の設計論には、純粋なランダムより解読可能な構造を重視する立場があった。

### Mechanism

規則を読む余地があると、
失敗 → 仮説 → 再試行 → 改善
というループが成立する。

純粋なランダムで結果が決まりすぎると、この学習ループが弱くなる。

### Generalized principle

**ランダムは問題の形を変えるために使い、学習可能性を消さない。**

---

## Observation G — Difficulty was also an operational parameter

アーケード基板には、難易度やボーナス条件などを運営側が調整できるものが存在した。

また当時の運営者の議論からは、初心者が最初の数分は遊べることと、熟練者が長時間占有しすぎないことの両立が経営上の課題だったことが読み取れる。

### Mechanism

難易度は一つの値ではない。

- 初心者が核へ触れるまでの猶予
- 熟練者へ要求する精度
- プレイ時間
- リソース供給
- パターン複雑度

を分けて考える必要がある。

### Generalized principle

**難易度を「ゲーム速度」一本で調整しない。**

---

## New playtest questions

- プレイヤーは敵の未来位置を予測できるか
- 成功した理由が0.5秒以内に伝わるか
- 大きな成功の後に呼吸できるか
- 色・点滅・音で危険優先順位が分かるか
- ランダム結果ではなく規則を学んで上達できるか
- EasyとHardで単に速度やHPだけが変化していないか
- 初心者が面白さの核へ触れる前に失敗していないか
