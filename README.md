# 🔧 車部品在庫管理アプリ

車部品の在庫を音声入力で簡単に登録・管理するWebアプリです。

## 機能

- 🎤 **音声入力** - Web Speech API を使用した音声認識（日本語対応）
- 🖊️ **手入力** - フォームでの手入力にも対応
- 🔍 **検索・管理** - 品名・品番などで検索可能、修正・削除機能
- ⚙️ **項目管理** - 管理者が項目を動的に追加・編集・削除可能
- 💾 **クラウドDB** - Supabase を使用した安全なデータ保管

## 入力項目（音声入力時の質問順）

1. 品名
2. 品番
3. 数量
4. 単価
5. 仕入先
6. メーカー
7. カテゴリ
8. 状態
9. 色
10. メモ

**スキップ方法**: 回答せず「次」と言うとその項目は空欄のまま次へ進みます。

## 技術スタック

- **フロントエンド**: HTML5 / CSS3 / Vanilla JavaScript
- **音声API**: Web Speech API (SpeechRecognition / SpeechSynthesis)
- **データベース**: Supabase (PostgreSQL)
- **認証**: Supabase Auth
- **ホスティング**: GitHub Pages

## セットアップ

### 1. Suabase 設定

1. [Supabase](https://supabase.com) でアカウント作成
2. 新しいプロジェクト作成
3. 以下のテーブルを SQL で作成:

```sql
-- fields_config テーブル（項目定義）
CREATE TABLE fields_config (
  id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  field_key TEXT UNIQUE NOT NULL,
  field_label TEXT NOT NULL,
  display_order INT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- items_master テーブル（商品データ）
CREATE TABLE items_master (
  id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  data JSONB NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

4. `index.html` 内の以下を更新:
   - `SUPABASE_URL` を自分のプロジェクト URL に変更
   - `SUPABASE_KEY` を自分の公開可能キーに変更

### 2. GitHub Pages デプロイ

1. GitHub に新しいリポジトリを作成（public）
2. リポジトリの **Settings** → **Pages**
3. **Source** を `Deploy from a branch`
4. **Branch** を `main` (or `master`) / `/ (root)` に設定
5. Save

リポジトリ URL: `https://github.com/YOUR_USERNAME/car-parts-inventory`  
公開 URL: `https://YOUR_USERNAME.github.io/car-parts-inventory/`

## 使い方

### 音声入力で登録

1. **🎤 音声で追加** ボタンをクリック
2. マイクボタンを押して各項目に回答
3. 「次」と言うと次の項目へ進む
4. すべての項目が終わると自動保存

### 手入力で登録

1. **＋ 手入力で追加** ボタンをクリック
2. フォームに項目を入力
3. **保存** ボタンでデータベースに保存

### 項目管理（管理者用）

1. **項目管理** ボタンをクリック
2. 項目の追加・編集・削除・表示順変更が可能
3. **保存** で反映

## ブラウザ対応

- Chrome / Chromium（推奨・音声認識対応）
- Edge
- Safari（音声機能は限定的）

## 注意事項

- 音声認識は HTTPS または `localhost` での実行が必要です
- ファイラー（「えーと」「あのー」など）は自動除去されます
- すべてのデータは Suabase に保存されます

## ライセンス

MIT License

## サポート

問題が発生した場合は、ブラウザのコンソールで詳細を確認してください。
