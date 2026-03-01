---
layout: post
title: "AIも人間も同じループを回している ── では、何が違うのか"
date: 2026-03-01
tags: [ai, llm, agents, philosophy]
description: "LLMと人間を閉ループ状態機械として比較し、差分の本質を『価値と更新の閉包』として再定義する。"
og_image: "/assets/ogp/default.png"
math: true
---

## アブストラクト

「LLMはステートレス、人間はステートフル」 ── この対比は入口に過ぎない。

ハーネス（外部メモリ、ツール、評価器、規約）込みで見れば、LLMエージェントも人間も**閉ループの状態機械**として同型だ。観測を受け取り、内部状態を更新し、行動し、環境を変え、次の観測を得る。外部に状態を持つ点も共通する。

だが差分は消えない。問題は「ステートの有無」から**「価値と更新がどこに閉じているか」**へ移る。

人間は外部ツールを使っても、価値・学習・コストの閉包が比較的強く個体に帰属し続ける。現代のAIエージェント系では、価値と更新が複数の最適化主体に分散し、統合の主体単位が曖昧になる。

AIに「主体性」や「機能意識」を実装する最難関は、能力の不足ではない。**価値と更新の閉包をひとつの系の内部にどう作るか、すなわち「主体の個体化」（individuation）の設計問題だ。**

本稿では、この結論に至る道筋を「同型性 → 差分 → 含意」の順に展開する。

---

## 1. 入口：ステートレス／ステートフルは何を言っていて、何を言い損ねるか

LLMと人間の知能を比べようとするとき、まず思いつく対比がある。

*「LLMはステートレスだ。入力を受け取り、推論し、出力する。一方、脳はステートフルで、経験が不可逆に刻まれていく。」*

ここでの「ステートレス」には、二つの異なる定義がある。

- **会話状態（context）の意味でのステートレス**：APIの1リクエストは独立で、会話を継続したいなら過去の入出力を次の入力に同梱する必要がある。OpenAIはこの "会話状態の管理" を明確な設計課題として扱っている。<sup><a href="#ref-1">(1)</a></sup>
- **学習（重み更新）の意味でのステートレス**：推論（inference）と学習（training）が分離されている。推論時にモデルの重みは固定され、どんな入力を受け取っても書き換わらない。<sup><a href="#ref-2">(2)</a></sup>

「会話履歴がなければ『さっきの自分』は存在しない」は、この定義の下ではかなり正確だ。

一方、人間の脳は対照的に見える。シナプス可塑性（長期増強 LTP と長期抑圧 LTD）により、経験は注意・記憶・情動・習慣といった複数の層で同時に、しかも自動的に内部状態を書き換える。<sup><a href="#ref-3">(3)</a>, <a href="#ref-4">(4)</a></sup> LLMが「外から文脈を渡されなければ前回の自分を知らない」のに対し、人間は「経験するだけで、本人の意図とは無関係に、複数の時間スケールで内部状態が更新され続ける」。しかもその更新コストは常に同一の身体が引き受ける。疲労し、忘れ、時に傷つく。

この非対称性が「ステートレス／ステートフル」の直観的な差を生んでいる。だが、この対比は**比較の軸としては粗すぎる**。LLMは単体で裸のまま動いていないし、人間も脳だけで知能を完結させていない。

---

## 2. 比較の土台を揃える：どちらも「閉ループの状態機械」として見られる

### 同型性の骨格

現実のLLMは、マルチターン会話のコンテキスト管理、外部メモリ、ログ、要約、ツール呼び出し、評価器、安全フィルタなど、モデルの「外側」に積み重なった仕組みとともに動いている。この外側の仕組み全体を、ここでは**ハーネス**と呼ぶ。LLM単体は会話状態の意味ではステートレスでも、ハーネス込みのシステムは十分にステートフルになり得る。

すると、LLMエージェントと人間（あるいは社会性昆虫）は、どちらも同じ骨格を持つように見えてくる。

**観測 → 内部状態更新 → 行動 → 環境変化 → 次の観測**

制御理論で言う閉ループの状態機械だ。この水準では、LLMエージェントも人間も**同型**である。

### 人間の「外部ハーネス」

人間は脳だけで知能を完結させているだろうか？ TODOリスト、ノート、スマートフォン、インターネット、言語、法律、制度、教育。これらはすべて「外部に状態を保持し、個体の判断と行動を変える仕組み」だ。認知が頭蓋内に閉じるという直観に対し、道具との結合を"心の一部"として扱う**拡張心説**（Extended Mind）が提示されている。<sup><a href="#ref-5">(5)</a></sup>

航海や操縦のような実作業では、個体の頭の中よりも「人・道具・表記・手順」の結合した系として認知を捉える**分散認知**の枠組みが詳細に記述されている。<sup><a href="#ref-6">(6)</a></sup> そして、テトリスの熟練者が頭の中で回転を計算する代わりに実際にブロックを回して見え方を変えるように、外界を書き換えて認知負荷を下げる行為は **epistemic action** と呼ばれる。<sup><a href="#ref-7">(7)</a></sup>

### スティグマジー：環境を外部メモリとして使う

この構図は人間に限らない。社会性昆虫では、個体が環境に痕跡を残し、その痕跡が次の行動を誘発する間接協調が古典的に定式化されている（**stigmergy**）。<sup><a href="#ref-8">(8)</a>, <a href="#ref-9">(9)</a></sup> アリの採餌で見られるフェロモントレイルは、探索の途中経過を環境側に保持して他個体の行動を変える仕組みとして実験・モデル化されている。<sup><a href="#ref-10">(10)</a>, <a href="#ref-11">(11)</a></sup>

![アリの画像](/assets/images/2026-02-28-ai-agents/pexels-estiak-11942105.jpg)
> Photo: [Estiak Jahan](https://www.pexels.com/photo/11942105/) (Pexels)

ここまでの要点：LLMエージェント、人間、社会性昆虫のいずれも「閉ループの状態機械＋外部ハーネス」という骨格を共有する。では差分はどこにあるか。

---

## 3. AI側の一次情報：ハーネスが更新則になっている

現代のコーディングエージェントでは、モデルの振る舞いを決めている要因の多くが**モデルの外側**にある。OpenAIもAnthropicも、この外側の仕組みを明確な設計対象として言語化している。<sup><a href="#ref-12">(12)</a></sup> その設計対象は、大きく4つの軸に整理できる。

- **規約の注入**：どんなルールがどの順序で読み込まれ、どの範囲に効くか
- **成果物の固定**：要件やテスト計画が次の入力として残り、工程を安定させる
- **観測の外部化**：トレースやログで何が起きたかを記録し、後から振り返れるようにする
- **行為空間の設計**：何ができて何ができないかを、権限やツールの境界で外から定める

根底にあるのは、エージェントを一発の関数呼び出しではなく**閉ループの計算**として捉える視点だ。推論→ツール呼び出し→結果の観測→次の推論。このループの中でどの情報がコンテキストに積み上がるかが、エージェントの振る舞いを決める。<sup><a href="#ref-13">(13)</a></sup>

### 規約の注入

OpenAI CodexのAGENTS.mdもAnthropic Claude CodeのCLAUDE.mdも、単なるドキュメントではなく、優先順位・スコープ・結合規則が仕様として定められた設定機構だ。<sup><a href="#ref-14">(14)</a>, <a href="#ref-16">(16)</a></sup> 権限やフックの設定も、属人的な運用ではなくスコープと優先順位で制御される仕組みになっている。<sup><a href="#ref-17">(17)</a></sup>

### 行為空間の設計

サンドボックスや権限管理は、モデルの能力以前に、行為の範囲そのものを外側から画定する。Codexのクラウド版はリポジトリが入ったサンドボックスでタスクを実行する前提が説明されており<sup><a href="#ref-20">(20)</a>, <a href="#ref-21">(21)</a></sup>、Claude Codeのサンドボックスも同様にモデルの行為空間を外側から制約する。<sup><a href="#ref-18">(18)</a></sup>

![Claude Code sandboxing](https://www-cdn.anthropic.com/images/4zrzovbb/website/0d1c612947c798aef48e6ab4beb7e8544da9d41a-4096x2305.png)
> 出典: Anthropic, "Making Claude Code more secure and autonomous with sandboxing" <sup><a href="#ref-18">(18)</a></sup>

### 成果物の固定と観測の外部化

マルチエージェントのワークフローでは、REQUIREMENTS.mdやTEST\_PLAN.mdといった成果物が工程間の引き継ぎ点になり、トレースやログが事後の振り返りと評価を可能にする。<sup><a href="#ref-15">(15)</a></sup>

### 見えない知は存在しない

モデルは訓練データから膨大な知識を内部に持っているが、ある作業で実際に使える知識は、ハーネスがコンテキストとして渡したものだけだ。プロジェクトのコード規約も、直前のテスト結果も、ハーネスが渡さなければモデルにとっては存在しないのと同じになる。<sup><a href="#ref-12">(12)</a></sup>

![見えない知は存在しない](https://images.ctfassets.net/kftzwdyauwt9/7uWHsJIC6o3uQPsnQ2Avz9/8be3e321892054bd215afb2b250a176a/OAI_Harness_engineering_The_limits_of_agent_knowledge_desktop-light.png)
> "What Codex can't see doesn't exist" ── OpenAI, "Harness engineering" <sup><a href="#ref-12">(12)</a></sup>

これらの具体例が指し示す傾向はひとつだ。**エージェントの振る舞いを安定させ改善するための制御（何をルールとし、何を記録し、何を許すか）は、モデルの重みの中ではなく、その外側に置かれている。**

---

## 4. 人間側の一次情報：更新則が「身体内」に高密度に実装されている

2章で見た通り、人間も外部ハーネスを使う。ここでは人間に固有の特徴、つまり**差分**だけに絞る。

### 可塑性（学習）が推論と分離していない

人間の脳では、推論と学習が密に絡み合い、同一の神経回路上で同時に走る。長期増強（LTP）と長期抑圧（LTD）は、シナプス結合の強度を経験依存的に変化させ、記憶の形成と忘却の基盤を成す。<sup><a href="#ref-3">(3)</a></sup> さらに、シナプス可塑性は単一メカニズムではなく、時間スケール（ミリ秒〜年単位）と神経回路（海馬・皮質・扁桃体・小脳）をまたぐ複合体として整理されている。<sup><a href="#ref-4">(4)</a></sup>

海馬リプレイ（覚醒時の経験を睡眠中やオフライン時に再生する仕組み）は、短期の経験を長期記憶に統合し計画に利用するメカニズムとして広く研究されている。<sup><a href="#ref-23">(23)</a></sup> つまり、「推論しながら同時に学習する」だけでなく、「休んでいる間にも過去の経験を再構成して学習する」プロセスが同一個体の内部で自動的に走る。

### コストが同一個体に帰属する

人間の学習を駆動するシグナルの中核に**報酬予測誤差**がある。期待した結果と実際の結果のずれが、ドーパミン系を介して行動方策の更新に直結する。<sup><a href="#ref-24">(24)</a></sup>

重要なのは、この誤差が身体を通じて主体に「返ってくる」ことだ。疲労、損傷、回復コストはすべて同一個体に帰属し、学習圧として作用する。AIエージェントでは同種のコスト（計算費用、信用毀損、権限剥奪）が複数の主体（開発組織、ユーザー、インフラ）に分散するが、人間ではこの帰属が個体内に強く閉じている。

---

## 5. 差分の定式化：閉包性（closure）

ここまでの同型性（2章）と差分（3・4章）を、数式で定式化する。

### 共通の骨格

まず、人間にもAIエージェントにも共通する閉ループの**最小形**を固定する。

$$
s_t = u(s_{t-1},\, o_t), \quad v_t = f(s_t), \quad a_t \sim \pi(\cdot \mid s_t,\, v_t)
$$

$$
o_{t+1} = \mathrm{Env}(a_t), \quad \delta_{t+1} = \mathrm{compare}(v_t,\, o_{t+1}), \quad \theta_{t+1} = \theta_t + \Delta(\delta_{t+1},\, \ldots)
$$

各記号の意味は以下の通り。

| 記号 | 意味 |
|---|---|
| $$o_t$$ | 時刻 $$t$$ の観測（感覚入力、ログ、テキスト入力など） |
| $$s_t$$ | 内部状態（belief state / 意思決定のための要約） |
| $$v_t = f(s_t)$$ | 価値変数（その状態がどれくらい良い／危険／望ましいか） |
| $$a_t$$ | 行動（ファイル編集、発話、身体運動など） |
| $$\pi$$ | 方策（状態と価値を受けて行動を出力する関数） |
| $$\mathrm{Env}$$ | 環境の応答関数。行動 $$a_t$$ を受け取り、次の観測 $$o_{t+1}$$ を返す |
| $$\mathrm{compare}$$ | 評価関数。内部の価値 $$v_t$$ と実際の結果 $$o_{t+1}$$ を突き合わせ、誤差 $$\delta_{t+1}$$ を算出する |
| $$\delta_{t+1}$$ | 評価誤差（期待と結果のずれ。RLなら報酬予測誤差、制御理論なら制御誤差、FEPなら予測誤差） |
| $$\theta$$ | 方策や価値関数のパラメータ（学習で変わる部分） |
| $$\Delta$$ | 更新則（誤差をパラメータ修正に変換する関数） |

### 三段の時系列：Encode → Act → Adapt

この骨格は、三つの段階として読める。

**Encode（観測・状態化・評価）：**

$$
o_t \;\longrightarrow\; s_t = u(s_{t-1},\, o_t) \;\longrightarrow\; v_t = f(s_t)
$$

知覚入力を「世界の状態」として内部表現にするプロセスと、その見立てに価値判断を与えるプロセスの二段だ。

**Act（行動選択）：**

$$
a_t \sim \pi(\cdot \mid s_t,\, v_t)
$$

価値 $$v_t$$ が行動を因果的に曲げる。

**Adapt（結果→誤差→更新）：**

$$
o_{t+1} = \mathrm{Env}(a_t), \quad \delta_{t+1} = \mathrm{compare}(v_t,\, o_{t+1}), \quad \theta_{t+1} = \theta_t + \Delta(\delta_{t+1},\, \ldots)
$$

$$\delta$$ は枠組みによって名前が異なる（RLでは報酬予測誤差、制御理論では制御誤差、FEPでは予測誤差）が、「期待と現実のずれ」という構造は共通だ。

### Encode / Act / Adapt を分離して描く利点

なぜ Encode を二段（$$u$$ と $$f$$）に分けるのか。$$u$$ は「世界をどう見立てるか」（状態推定）、$$f$$ は「その見立てにどう価値判断を与えるか」（評価）だ。この二つを分離しておくと、**閉包性の議論で決定的な差分が見える**ようになる。

コーディングエージェントでは、「世界の見立て」にあたる $$u$$（会話履歴やコード差分の蓄積）はセッション内部で回る。しかし「何が良いか」の基準にあたる $$f$$（テスト仕様、コーディング規約、approval policy）はAGENTS.mdやテストハーネスとして**エージェントの外側**に置かれることが多い。さらに、誤差をパラメータ修正に変換する更新則 $$\Delta$$ も、LLMの重みではなく外部の成果物（コミット、メモ、規約ファイル）に流れる。

人間では事情が異なる。「世界の見立て」（$$u$$: 知覚・記憶の統合）も、「何が良いか」の基準（$$f$$: 快・不快、欲求、規範の内面化）も、「誤差から学ぶ仕組み」（$$\Delta$$: シナプス可塑性による方策更新）も、すべてが同一の身体・神経系の内部で高密度に結びついている。

つまり、$$u$$, $$f$$, $$\Delta$$ を分けて書くことで、「どの関数がどこに住んでいるか」を問えるようになる。**同じ閉ループの骨格を共有しながら、関数の所在が異なる**。これが閉包性の差を記述する鍵になる。

### 比較すべき四つの軸

差分を特定するために、以下の四軸で比較する。

| 軸 | 問い |
|---|---|
| **State**（状態） | 内部状態 $$s_t$$ はどこに保持されるか |
| **Update**（更新則） | $$u, f, \pi$$ はどこで・どう修正されるか |
| **Value**（価値） | 何が最適化されているか、$$v_t$$ の帰属先は |
| **Timescale**（時間スケール） | 更新がどの時間スケールで統合されているか |

### マッピング：コーディングエージェント vs. 生物脳

同じ数式の各変数が、具体的にどう対応するか。コーディングエージェントの代表例としてOpenAI Codexを取り上げ、生物脳と並べる。

<div style="overflow-x: auto;">
<table>
<thead>
<tr><th>変数</th><th>OpenAI Codex</th><th>生物脳</th></tr>
</thead>
<tbody>
<tr>
<td markdown="span">$$o_t$$（観測）</td>
<td>ユーザー指示＋リポジトリ状態（ファイル内容）＋コマンド実行結果＋テスト結果。ローカルの選択ディレクトリ内で「読める・書ける・実行できる」前提 <sup><a href="#ref-19">(19)</a></sup></td>
<td>感覚入力（視覚・聴覚・内受容感覚など）</td>
</tr>
<tr>
<td markdown="span">$$s_t = u(s_{t-1}, o_t)$$（状態）</td>
<td>会話履歴＋ファイル差分＋ツール結果＋要約の合成。AGENTS.md が初期条件（事前コンテキスト）として効く <sup><a href="#ref-14">(14)</a></sup>。sandbox と approval policy が観測・行為の範囲を制約 <sup><a href="#ref-21">(21)</a></sup></td>
<td>強いステートフル性（反回路＋記憶系）。海馬リプレイが過去の経験を圧縮して運ぶ <sup><a href="#ref-23">(23)</a></sup></td>
</tr>
<tr>
<td markdown="span">$$v_t = f(s_t)$$（価値）</td>
<td>「テストが通る・要求を満たす・安全制約に違反しない・スタイル規約に従う」といった評価軸。多くは AGENTS.md／指示文／approval policy／テストハーネスとして<strong>外部に</strong>実装 <sup><a href="#ref-14">(14)</a></sup></td>
<td>接近／回避、快・不快、欲求、危険度など、評価機構の合成。報酬予測誤差が学習の中核シグナル <sup><a href="#ref-24">(24)</a></sup></td>
</tr>
<tr>
<td markdown="span">$$\mathrm{Env}$$（環境）</td>
<td>リポジトリ＋ファイルシステム＋CI/CD＋外部API。クラウド版はsandbox内でタスク実行 <sup><a href="#ref-20">(20)</a></sup></td>
<td>物理世界＋社会環境＋道具</td>
</tr>
<tr>
<td markdown="span">$$a_t$$（行動）</td>
<td>ファイル編集、コマンド実行、PR作成</td>
<td>身体運動、発話、道具操作</td>
</tr>
<tr>
<td markdown="span">$$\mathrm{compare}$$（評価）</td>
<td>テスト実行結果との照合、lint、ビルド成否判定、approval policy による可否判定</td>
<td>報酬予測誤差（ドーパミン系）、体性感覚フィードバック、情動的評価</td>
</tr>
<tr>
<td markdown="span">$$\delta$$（誤差）</td>
<td>テスト失敗、ビルド失敗、lint警告、ユーザーの否定フィードバック、approval拒否</td>
<td>報酬予測誤差シグナル、制御誤差、痛み信号</td>
</tr>
<tr>
<td markdown="span">$$\theta$$ と $$\Delta$$（パラメータと更新）</td>
<td>セッション内ではLLM重み \(\theta\) は固定。更新は主に<strong>外部状態</strong>へ流れる：修正コミット、メモ書き、AGENTS.md追記。MCP化で外部状態の持続を強化可能 <sup><a href="#ref-25">(25)</a></sup></td>
<td>誤差がシナプス可塑性＝パラメータ更新に<strong>直結</strong>。LTP/LTD が長期的な結合強度を変化させる <sup><a href="#ref-3">(3)</a></sup></td>
</tr>
</tbody>
</table>
</div>

### 閉包性の差分

このマッピングから浮かび上がる差分を、一文で言い切る。

- **生物脳**：Adapt段階（誤差→更新）が境界内で $$\theta$$ に落ちる。学習・コストが同一個体に帰属する。
- **コーディングエージェント**：Adaptは主に外部状態（コード、メモリ、規約ファイル、テストハーネス、approval）へ流れ、$$\theta$$ 更新は境界外（モデル運営側）にあることが多い。

さらに、外部状態を積めば賢くなるとは限らない。Long-context LLMの評価では、関連情報がプロンプトの「真ん中」に位置するだけで検索精度が著しく落ちる "lost in the middle" 現象が示されている。<sup><a href="#ref-26">(26)</a></sup> 長期記憶を階層化して必要なものだけをプロンプトに "ページイン" する設計も、OS的な発想として提案されている。<sup><a href="#ref-27">(27)</a></sup> つまり、ステートフルにすること自体は容易だが、蓄積した状態を正しく使えるかは別の問題であり、ここにもハーネス設計の難しさがある。

---

## 6. 価値を認識する条件 → 痛み（機能） → 二階ループ

### 三本の矢印：Encode → Act → Adapt

前章の数式を使って、「ある系が価値を持つとはどういうことか」を考える。

5章で定義した Encode, Act, Adapt の三段は、条件のチェックリストというより、**閉ループが閉じるために必要な3本の矢印**として読める。

**矢印A（Encode）：価値が内部変数として立つ**

$$
s_t \;\longrightarrow\; v_t = f(s_t)
$$

内部に「どうあるべきか」の規範・評価が存在する。これがなければ比較の基準が立たず、誤差を系の内部で定義できない。価値は観測者が外から貼るラベルにとどまる。

**矢印B（Act）：その価値が行動を因果的に曲げる**

$$
a_t \sim \pi(\cdot \mid s_t,\, v_t)
$$

価値が行動を変えなければ、ループは価値を経由せずに閉じる。心の哲学で言うエピフェノメノン、つまり存在はしても因果的に働かない副産物だ。

**矢印C（Adapt）：誤差が更新に接続される**

$$
\delta_{t+1} = \mathrm{compare}(v_t,\, o_{t+1}), \quad \theta_{t+1} = \theta_t + \Delta(\delta_{t+1},\, \ldots)
$$

誤差が出ても更新されないなら、固定方策の反射機械は作れても、価値が更新則として機能しているとは言いがたい。

三本の矢印を一文にまとめる。

> **ある系が価値を持つとは、(A) 価値がその系の内部に表現され、(B) それが行動を制御し、(C) 結果との誤差が系自身の更新に戻る、というフィードバック経路が閉じていることだ。**

こう整理すると、A/B/Cは恣意的なチェックリストではなく、閉包性（value / learning / cost が境界内で閉じること）を記述する**最小回路図**になる。

### 条件Cと二階の閉ループ

条件Cは、直観的には**二階の閉ループ**に相当する。

- **一階のループ**：行動 → 結果 → 行動の調整
- **二階のループ**：行動を生む方策 → 方策の評価 → 方策の修正

人間の学習は、少なくともこの二階のループを多様な形で回している。火傷をした子供は、火に近づく行動を避けるだけでなく、「高温のものは危険だ」という方策そのものを獲得する。

### 「痛み」を機能として定義する

条件Cを掘ると、痛みの問題に突き当たる。

人間は有限で、失敗は身体に返り、回復にはコストがかかる。だから学習の動機がある。ではAIエージェントはどうか。権限を剥奪されても、予算を削られても、信用を失っても、それは「痛い」のか。

ここで問題にしたいのは痛みの**クオリア**（主観的な感覚）ではなく、痛みが果たしている**制御機能**だ。機能としての痛みには少なくとも三つの役割がある。

1. **回避行動を強制する。**
2. **注意と学習モードを切り替える**（通常モードから警戒モードへ）。
3. **失敗の再発を下げる更新に接続される。**

「失敗コストが主体に帰属する」とは、機能的に言えば、**失敗がその主体の将来の行動可能性を実際に狭め、回復に実コストがかかり、その制約が内部の意思決定と更新に因果的に戻る**ことだ。

数式で言えば、Adapt段階の $$\Delta$$ が $$\theta$$ を実際に書き換え、かつその書き換えのコスト（計算量、不可逆性、痛み信号）が同一の系に帰属するということになる。人間ではこの帰属が強い。AIエージェント系では、前章で見た通り $$\Delta$$ の多くが外部に散逸する。これが、条件Cが最難関である理由だ。

---

## 7. 系全体で見れば二階ループは回っている

個々のセッションでは、AIエージェントは条件Cを強い意味で満たしにくい。しかし**系全体**に視野を広げるとどうか。

ユーザーがエージェントを使い、失敗事例が蓄積され、開発チームがそれを分析し、モデルやハーネスが更新される。この「外側の学習」は開発プロセスとして実際に行われている。<sup><a href="#ref-29">(29)</a></sup> RLHFでは人間のフィードバックでモデルをファインチューニングし、振る舞いを更新する枠組みが示されている。<sup><a href="#ref-28">(28)</a></sup> ツール使用の学習も研究として存在する。<sup><a href="#ref-30">(30)</a></sup>

セッション単体のLLMは変わらなくても、「LLM＋ハーネス＋開発組織＋ユーザーフィードバック」という系全体は失敗を内在化し続けている。二階の閉ループは、セッション内ではなく**eval → 改善 → 再評価**という外部学習として回っている。

この視点に立てば、AIも人間も「拡張主体」として閉ループを回していることになる。人間も言語や制度やインターネットという外部ハーネスなしには現在の知能を維持できない。<sup><a href="#ref-5">(5)</a>, <a href="#ref-6">(6)</a></sup>

ただし、こう広げた途端に「誰がoptimizerか」が曖昧になる。ユーザー、開発組織、モデル、ハーネスのうち、どれが方策を更新する主体なのか。

---

## 8. 主体の再定義：optimizerと閉包性

### 主体＝optimizer

「主体」「アクター」「エージェント」といった語は日常的に使われるが、ここまでの議論には曖昧すぎる。本稿では**主体＝optimizer**と定義する。optimizerとは、行動を出力するだけでなく、目的関数に沿って自らの方策を更新する実体だ。行動を返すだけなら関数で足りる。更新するからoptimizerと呼ぶ。

この定義で7章を振り返ると、「系として見れば同型」の裏に隠れていた差分が見えてくる。

**人間（＋外部ハーネス）**では、更新は基本的に同一の個体に帰属し続ける。外部ツールは同一optimizerの手足や記憶の延長だ。<sup><a href="#ref-5">(5)</a></sup>

**現代のAIエージェント系**では、更新と目的が複数のoptimizerに分裂する。ユーザーの要求、開発組織のポリシー、市場の圧力、規制当局の要件、モデルの方策は互いに独立した最適化主体であり、しばしば矛盾する目的を持つ。エージェントの出力は、これらの交渉と妥協の結果だ。

人間の外部ハーネスが「**同一optimizerの外部メモリ化**」であるのに対し、AIの外部ハーネスは「**異なるoptimizerの介入と交渉の場**」になる。

### 人間も一枚岩ではない：差は統合の度合い

ここで当然の反論が出る。人間だって一枚岩のoptimizerではない。衝動と理性は矛盾し、短期的快楽と長期的目標は対立し、恐怖反応は意識的判断を飛ばして走る。

たしかにそうで、人間も内部に複数の準最適化ループを抱えている。だとすれば問題は「optimizerが単一か複数か」ではなく、**統合の度合い**だ。

統合は0か1のスイッチではなく連続的な量であり、より正確には**閉包性（closure）**と呼べる。複数の最適化ループがあっても、それらがある境界の内側で強く結合し、**価値・学習・コストの帰属がその範囲に閉じている**なら、その系は統合されていると言える。

人間の場合、衝動と理性が矛盾しても、最終的にはひとつの身体がひとつの行動を選ぶ。学習は同一の神経系に蓄積される。<sup><a href="#ref-3">(3)</a></sup> 内部の葛藤がどれだけあっても、価値・学習・コストの閉包は比較的強く個体に帰属し続ける。これが人間における統合の基盤だ。

### Markov blanket：境界を扱う道具

この「境界」と「閉包性」を数学的に扱う道具として、**マルコフブランケット**（Markov blanket）がある。フリストンは、マルコフブランケットを「内部状態と外部状態を統計的に分離する境界」として導入している。<sup><a href="#ref-31">(31)</a></sup> この境界は、細胞から個体、さらには環境の一部を含む形まで、入れ子状に構成され得る（ "Markov blankets of Markov blankets" ）。<sup><a href="#ref-32">(32)</a></sup>

![マルコフブランケットの図](/assets/images/2026-02-28-ai-agents/markov-blanket.svg)
> Diagram of a Markov blanket by Laughsinthestocks (CC0, Wikimedia Commons)

社会や組織もまた、より緩やかなブランケットとして記述できる可能性がある。<sup><a href="#ref-32">(32)</a></sup> どのレベルの閉包を「主体」と呼ぶかは、分析の目的に依存する。

5章の数式に戻れば、マルコフブランケットは「$$s_t, v_t, \theta$$ のどこまでがブランケットの内側にあり、$$\Delta$$ がその内側で閉じているか」を問う枠組みだ。人間は $$\{s, v, \theta, \Delta\}$$ が比較的強く同一ブランケット内に収まる。AIエージェント系では $$\theta$$ と $$\Delta$$ がブランケットの外に散る。

---

## 9. 結語：問いの置き場

本稿の論旨をまとめる。

1. **同型性**：ハーネス込みで見れば、LLMエージェントも人間も「観測→状態→価値→行動→環境→次の観測」という閉ループの状態機械として同型だ。
2. **差分**：差分は「ステートの有無」ではなく、**価値と更新がどこに閉じているか（閉包性）にある**。人間では $$\{v, \theta, \Delta\}$$ が個体内に高密度に閉じる。AIエージェント系では $$\theta$$ と $$\Delta$$ が外部に分散する。
3. **含意**：AIに「主体性」や「機能意識」を実装する最難関は、能力の不足ではない。**閉包性をどう設計するか、すなわち主体の個体化（individuation）の問題だ。**

この見方が正しいなら、次に問うべきは「閉包性を強める設計パターンとは何か」だ。たとえば、失敗のコストをエージェント自身に帰属させる仕組み、学習結果を同一の系に蓄積する長期メモリ、価値基準の自己更新。課題は「AIをもっと賢くすること」ではなく、**価値・学習・コストがひとつの主体の内部で閉じるようにシステムを設計すること**だ。

この議論は**身体性（embodiment）**の問題と深く通じている。本稿で閉包性が人間において強い最大の理由は、身体があるからだ。コストが外部に逃げない。学習が同一の神経系に蓄積される。ひとつの身体がひとつの行動を強制する。身体こそが閉包の物理的な基盤になっている。とすれば、AIエージェントに閉包性を実装するとは、何らかの意味で「身体に相当するもの」を設計することなのかもしれない。物理的な身体である必要はないが、コストが蓄積し、学習が残り、行動の結果から逃れられない持続的な境界。エージェントにとっての身体とは何か、という問いが本稿の先に控えている。

---

## References

<ol class="references">
<li id="ref-1"><a href="https://developers.openai.com/api/docs/guides/conversation-state/">Conversation state | OpenAI API</a></li>
<li id="ref-2"><a href="https://developers.openai.com/api/docs/guides/your-data/">Data controls in the OpenAI platform | OpenAI API</a></li>
<li id="ref-3"><a href="https://pmc.ncbi.nlm.nih.gov/articles/PMC3118435/">Long-term potentiation and long-term depression (Bliss &amp; Collingridge, 2011) | PMC</a></li>
<li id="ref-4"><a href="https://www.nature.com/articles/1301559">Synaptic Plasticity: Multiple Forms, Functions, and Mechanisms (Citri &amp; Malenka, 2008)</a></li>
<li id="ref-5"><a href="https://www.alice.id.tue.nl/references/clark-chalmers-1998.pdf">The Extended Mind (Clark &amp; Chalmers, 1998)</a></li>
<li id="ref-6"><a href="https://direct.mit.edu/books/monograph/4892/Cognition-in-the-Wild">Cognition in the Wild (Hutchins, 1995)</a></li>
<li id="ref-7"><a href="https://adrenaline.ucsd.edu/kirsh/Articles/CogsciJournal/DistinguishingEpi_prag.pdf">On Distinguishing Epistemic from Pragmatic Action (Kirsh &amp; Maglio, 1994)</a></li>
<li id="ref-8"><a href="https://link.springer.com/article/10.1007/BF02223791">La théorie de la stigmergie (Grassé, 1959)</a></li>
<li id="ref-9"><a href="https://direct.mit.edu/artl/article/5/2/97/2318/A-Brief-History-of-Stigmergy">A Brief History of Stigmergy (Theraulaz &amp; Bonabeau, 1999)</a></li>
<li id="ref-10"><a href="https://link.springer.com/article/10.1007/BF01240531">Trail laying behaviour during food recruitment in the ant Lasius niger (Beckers et al., 1992)</a></li>
<li id="ref-11"><a href="https://link.springer.com/article/10.1007/BF01417909">The self-organizing exploratory pattern of the Argentine ant (Deneubourg et al., 1990)</a></li>
<li id="ref-12"><a href="https://openai.com/index/harness-engineering/">Harness engineering: leveraging Codex in an agent-first world | OpenAI</a></li>
<li id="ref-13"><a href="https://openai.com/ja-JP/index/unrolling-the-codex-agent-loop/">Unrolling the Codex agent loop | OpenAI</a></li>
<li id="ref-14"><a href="https://developers.openai.com/codex/guides/agents-md/">Custom instructions with AGENTS.md</a></li>
<li id="ref-15"><a href="https://developers.openai.com/cookbook/examples/codex/codex_mcp_agents_sdk/building_consistent_workflows_codex_cli_agents_sdk">Building Consistent Workflows with Codex CLI &amp; Agents SDK</a></li>
<li id="ref-16"><a href="https://docs.anthropic.com/en/docs/claude-code/memory">How Claude remembers your project - Claude Code Docs</a></li>
<li id="ref-17"><a href="https://docs.anthropic.com/en/docs/claude-code/settings">Claude Code settings - Claude Code Docs</a></li>
<li id="ref-18"><a href="https://www.anthropic.com/engineering/claude-code-sandboxing">Making Claude Code more secure and autonomous with sandboxing | Anthropic</a></li>
<li id="ref-19"><a href="https://developers.openai.com/codex/cli/">Codex CLI | OpenAI Developers</a></li>
<li id="ref-20"><a href="https://openai.com/index/introducing-codex/">Introducing Codex | OpenAI</a></li>
<li id="ref-21"><a href="https://developers.openai.com/codex/security/">Security | OpenAI Codex</a></li>
<li id="ref-22"><a href="https://code.claude.com/docs/en/overview">Claude Code overview - Claude Code Docs</a></li>
<li id="ref-23"><a href="https://pmc.ncbi.nlm.nih.gov/articles/PMC5847173/">The Role of Hippocampal Replay in Memory and Planning | PMC</a></li>
<li id="ref-24"><a href="https://pubmed.ncbi.nlm.nih.gov/9054347/">A neural substrate of prediction and reward (Schultz et al., 1997) | PubMed</a></li>
<li id="ref-25"><a href="https://developers.openai.com/codex/guides/agents-sdk/">Use Codex with the Agents SDK | OpenAI Developers</a></li>
<li id="ref-26"><a href="https://arxiv.org/abs/2307.03172">Lost in the Middle: How Language Models Use Long Contexts (Liu et al., 2023)</a></li>
<li id="ref-27"><a href="https://arxiv.org/abs/2310.08560">MemGPT: Towards LLMs as Operating Systems (Packer et al., 2023)</a></li>
<li id="ref-28"><a href="https://arxiv.org/abs/2203.02155">Training language models to follow instructions with human feedback (Ouyang et al., 2022)</a></li>
<li id="ref-29"><a href="https://developers.openai.com/api/docs/guides/model-optimization/">Model optimization | OpenAI API</a></li>
<li id="ref-30"><a href="https://arxiv.org/abs/2302.04761">Toolformer: Language Models Can Teach Themselves to Use Tools (Schick et al., 2023)</a></li>
<li id="ref-31"><a href="https://pubmed.ncbi.nlm.nih.gov/23825119/">Life as we know it (Friston, 2013) | PubMed</a></li>
<li id="ref-32"><a href="https://pubmed.ncbi.nlm.nih.gov/29343629/">The Markov blankets of life (Kirchhoff et al., 2018) | PubMed</a></li>
</ol>
