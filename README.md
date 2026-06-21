# 📊 成績管理

定期考査・模試の成績を記録し、推移をグラフで可視化できるWebアプリです。
Googleアカウントでログインすると、Firebase Realtime Database を通じてデータがクラウドに自動保存されます。

🔗 **公開URL**: https://kaicraft0518.github.io/seiseki/

---

## ✨ 主な機能

### 定期考査
- 学年（1年・2年・3年）× 考査回（第1回〜第4回）でデータを管理
- 科目ごとに「満点・目標点・平均点・自分の点数・学年最高点（任意表示）」を入力
- 平均点との差・目標点との差・得点率・評定（10段階）を自動計算
- 合計点・合計評定（手入力）・学年順位も記録可能
- 推移グラフ
  - 合計点の推移（自分・目標・平均を比較）
  - 科目別の評定推移、平均点との差の推移

### 模試
- 模試ごとに「総合」「国語」「数学」「英語」の点数・偏差値・順位を記録
- 点数推移グラフ・偏差値推移グラフを自動生成

### その他
- Googleログインによるユーザーごとのデータ分離
- 入力内容は自動保存（1.5秒のデバウンス後にFirebaseへ同期）
- スマホ対応レイアウト（横スクロール時も科目列が固定表示）
- ホーム画面への追加に対応（PWA簡易対応・アイコン設定済み）

---

## 🛠 技術構成

| 項目 | 内容 |
|---|---|
| フロントエンド | HTML / CSS / JavaScript（単一ファイル） |
| グラフ描画 | [Chart.js](https://www.chartjs.org/) |
| 認証 | Firebase Authentication（Googleログイン） |
| データベース | Firebase Realtime Database |
| ホスティング | GitHub Pages |

---

## 📁 ファイル構成

```
/index.html       … アプリ本体（HTML/CSS/JSすべて含む単一ファイル）
/icon.png         … アプリアイコン
/manifest.json    … PWA用マニフェスト
```

---

## 🚀 セットアップ（自分の環境で動かす場合）

1. [Firebase Console](https://console.firebase.google.com/) で新規プロジェクトを作成
2. **Authentication** → 「Sign-in method」で Google を有効化
3. **Realtime Database** を作成し、以下のルールを設定

   ```json
   {
     "rules": {
       "users": {
         "$uid": {
           ".read": "$uid === auth.uid",
           ".write": "$uid === auth.uid"
         }
       }
     }
   }
   ```

4. プロジェクト設定からウェブアプリを登録し、`firebaseConfig` を取得
5. `index.html` 内の `firebaseConfig` を自分の値に置き換える
6. Authentication の「承認済みドメイン」に GitHub Pages のドメインを追加
7. GitHub Pages で公開

---

## 📌 評定の計算方法

```
評定 = 得点率 × 9 + 1（1〜10の範囲に丸め）
```

満点が科目・考査ごとに異なっていても、得点率ベースで評定を算出します。

---

## ⚠️ 注意事項

- データはブラウザのlocalStorageではなく、Firebaseのクラウド上に保存されます
- ログインしていない状態ではデータの閲覧・編集はできません
- 複数端末から同じGoogleアカウントでログインすると、データはリアルタイムで同期されます

---

## 📄 ライセンス

個人利用・学習目的での利用を想定しています。