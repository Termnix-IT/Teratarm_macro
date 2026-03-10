# 日課取得マクロ（簡易版） Readme

■ 概要
本マクロは、Cisco系機器（IOS/NX-OS 等）にログインし、enable（特権モード）までを手動で実施した後、日課点検で利用する代表的な show コマンドを自動で実行する Tera Term マクロです。
最小構成で確実に動作することを目的としており、初期導入や簡易的な自動化に適しています。

■ 前提条件
・Tera Term がインストールされていること
・SSH または Telnet で対象機器へ接続できること
・ログイン後、手動で enable を実行してプロンプトを「#」にしておくこと
・機器が「terminal length 0」に対応していること（ページャ無効化）

■ 実行手順

Tera Term を使って対象機器へ接続します。
手動で enable を実行し、プロンプトが「#」であることを確認します。
Tera Term のメニュー［Control → Macro…］から本マクロ（.ttl）を選択し実行します。

※ マクロでは「#」または「>」をプロンプトとして待機しますが、基本は「#」での実行を前提としています。

■ マクロが実行するコマンド一覧

terminal length 0
show clock
show running-config
show archive config diff
show interface status
show etherchannel summary
show spanning-tree blockedports
show spanning-tree
show ntp status
show env all
show interface transceiver detail
show logging
exit

■ 安定実行のための補足
・terminal length 0 の直後に短い pause を入れると取りこぼしが減ります。
・show logging のみ timeout を長めに設定することで止まりにくくなります。
・大量のログ取得が不要な場合、「show logging | include %SYS-|%LINK-|%LINEPROTO-」などで絞り込むことも可能です。

■ 既知の制限事項
・本マクロは簡易版のため、エラー制御や分岐処理は実装していません。
・ログの自動保存（logopen/logclose）は未搭載です。必要に応じて後で追加してください。
・コマンド非対応時のエラーは画面に表示されますが、マクロは継続動作します。

■ カスタマイズ例（必要になったら）
・ログ保存機能の追加（logopen/logclose）
・コマンドごとに見出しを表示してログ可読性を向上
・機種／OS 差異（IOS、IOS-XE、NX-OS など）に応じた分岐
・enable 自動化（パスワードは外部ファイルで管理）

■ 変更履歴（例）
2026-02-12: 初版作成（簡易版マクロ運用開始）
