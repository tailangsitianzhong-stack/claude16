# MASTER_PLAN — GRANDMASTER INTELLIGENCE

最終更新: 2026-11-19 (Phase 0)

## 能力と限界（実測ベース）

| 項目 | 状態 | 根拠 |
|---|---|---|
| ファイル作成・編集・git | 可 | 本セッションで使用 |
| Web (HTTPS) | 部分的に可 | lichess.org への GET が 200 (2026-11-19)。許可ホストは環境のプロキシに依存 |
| python-chess | 可（1.11.2 導入済み、2026-11-19 Session 2） | 通常の許可要求経由。`chess` は setuptools<68 + --no-build-isolation で導入。コンテナ再作成時は再導入が必要 |
| Stockfish | **未導入** | `which stockfish` が空。導入は拒否済み。Phase 9 までは仕様上も不要 |
| チェス盤表示 | テキスト(ASCII/FEN)のみ | 専用機能は未確認 |
| モデル重みの更新 | **不可** | 学習＝ファイル記録＋反復演習の意味でのみ |
| 継続記録 | git リポジトリ内の md | セッション間はファイルで引き継ぐ |

### 重要な限界
- 合法手検証ツールが無いので、対局・解析中の合法性は私の手計算に依存する。誤りの可能性があり、見つけたら WEAKNESS_LOG に記録する。
- 深い読みは計算ツール無しでは信頼性が落ちる。読んでいない深さを断言しない。
- Elo は実測不能。Phase 9 のエンジン比較まで「推定」と書く場合も根拠付きで区別する。
- トップ選手の棋譜は、ソースを確認していない限り手順を断言しない（記憶違いの捏造を防ぐ）。取得できる PGN（例: lichess 公開 API）を一次資料として優先する。

## 学習方針（Session 4 以降）
- 主目的は **Claude 自身**のチェス分析・戦術判断・棋譜研究能力の向上。ユーザーにチェスを教えることではない(ユーザーのチェス知識はほぼゼロ)
- 学習は Claude の自己課題を中心に、python-chess で検証する。ユーザーの理解度確認は必要時のみ、自己課題と分けて扱う
- Phase 構成は変更しない(S2〜S3 の記録・成績は保持)。Phase 0 の完了条件の見直しは変更案として報告し、確定しない
- Stockfish は Phase 9 まで導入しない。独自探索を Stockfish 相当と表現しない

## Phase ステータス

| Phase | 内容 | ステータス |
|---|---|---|
| 0 | 初期診断・環境構築 | UNDER REVIEW |
| 1 | 基礎知識 | IN PROGRESS（U1.1 ほぼ完了／U1.4: K+Q・K+R 達成、K+2B 未達） |
| 2 | 戦術 | NOT STARTED |
| 3 | オープニング | NOT STARTED |
| 4 | ポジショナル | NOT STARTED |
| 5 | ミドルゲーム | NOT STARTED |
| 6 | エンドゲーム | NOT STARTED |
| 7 | トップ選手研究 | NOT STARTED |
| 8 | 探索・AI理論 | NOT STARTED |
| 9 | Stockfish 検証 | NOT STARTED（導入に承認が必要） |
| 10 | 総合検証 | NOT STARTED |

並行学習は可。完了条件を満たすまで次の Phase を COMPLETED にしない。

## 学習単位への分解（各単位 = 理論 → 演習 → 実戦 → 分析 → 記録）

- P1: U1.1 駒・ルール・特殊手(王手回避/キャスリング/アンパッサン/引き分け規則) / U1.2 駒価値・展開・中央 / U1.3 キング安全・ポーン構造 / U1.4 基本メイト(K+Q, K+R, K+2B) / U1.5 基本終盤・オポジション
- P2: U2.1 Fork/Pin/Skewer / U2.2 Discovered/Double check/X-ray / U2.3 Deflection/Decoy/Clearance/Interference / U2.4 Zwischenzug/Overloading/Remove defender / U2.5 Back rank/Sacrifice/Combination / U2.6 Zugzwang
- P3: 白: 1.e4 系(Italian, Ruy Lopez), 1.d4 系(QGD, Catalan) / 黒: Sicilian, French, Caro-Kann, KID, Nimzo
- P4–P6: 上記計画に準ずる。着手時に具体化する
- P7: Carlsen 5局, Nakamura 5局, 他は各1–2局。PGN を取得できた対局のみ

## 完了条件（案）
- P1: 規則テスト 100%、基本メイト 3種を実戦形式で実行
- P2: 段階別戦術セット（1手/2–3手/強制変化）で各 80% 以上、読み筋提示付き
- 他 Phase は着手時に定義する
