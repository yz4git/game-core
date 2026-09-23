# Photo Mode & Player Expression

Photo modeを「HUDを消して自由カメラにする機能」ではなく、ゲーム世界を再解釈して共有する第二の遊びとして設計する。

## 1. Reuse expressive world variables

ゲーム本編が持つ、
- time of day
- weather
- lighting
- pose
- animation state
- camera lens
を写真表現へ再利用する。

専用filterを大量追加する前に、既存世界の表現力を開放する。

## 2. Give the player authorship

良いphoto modeでは「綺麗な場所を撮った」だけでなく、
- framing
- timing
- juxtaposition
- weather choice
- pose
によって撮影者の意図が出る。

## 3. Integrate photography into the world when appropriate

写真を、
- wildlife discovery
- NPC request
- journal
- collection
- clue
と接続すると、撮影がメニュー外の遊びではなく本編の行為になる。

ただし純粋な自由撮影を妨げるほど義務化しない。

## 4. Preserve contextual memory

画像だけでなく任意に、
- recent dialogue
- location
- run time
- boss / event
- weather
- date
などを保存すると、後から意味を思い出しやすい。

## 5. Separate capture from decoration

撮影時:
- composition
- subject
- timing

撮影後:
- exposure
- tint
- frame
- caption

を分けると、リアルタイムの瞬間を逃さず編集できる。

## 6. Photo mode can be progression without power

写真機能の解禁や撮影対象収集は、戦闘力を上げない横方向progressionとして使える。

世界観への関心を報酬化できる。

## 7. Do not break art direction accidentally

自由度を増やしても、
- clipping
- unloaded LOD
- hidden backstage geometry
- broken animation
が露出すると作品品質を下げる。

camera boundsやphoto-specific LODを検討する。

## 8. Sharing should preserve intent

共有cardに、必要なら
- creator name
- location
- challenge/category
- game version
を含める。

UI watermarkを強くしすぎて写真そのものを壊さない。

## 9. Accessibility

photo mode操作にも、
- hold不要
- sensitivity
- reset camera
- motion reduction
- UI scaling
を考える。

## Playtest

- 10人が同じ場所で違う写真を作れるか
- filterを使わなくても構図だけで個性が出るか
- 写真を見て撮影時の出来事を思い出せるか
- free cameraで未完成領域が頻繁に露出しないか
- photo objectiveが本編探索を豊かにしているか
- 撮影開始／終了がゲームテンポを壊しすぎないか
