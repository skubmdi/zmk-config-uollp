# zmk-config-uollp ZMK Config Template

このリポジトリは、自作キーボード [skubmdi/uollp](https://github.com/skubmdi/uollp) 用の ZMK ファームウェアを  
GitHub Actions 等でビルドするための **テンプレートリポジトリ** です。

> [!NOTE]
> 本リポジトリにはキーボードの定義（Shield）は含まれておらず、  
> 別リポジトリ [skubmdi/zmk-keyboard-uollp](https://github.com/skubmdi/zmk-keyboard-uollp) を `west.yml` 経由でモジュールとして読み込む構成になっています。

## 使い方 (Getting Started)

### 1. リポジトリをフォーク (Fork)

1. ページ右上にある **[Fork]** ボタンをクリックします。
2. **Repository name** を `zmk-config-uollp-template` から末尾の `-template` を削除し、`zmk-config-uollp` に変更します。
3. **[Create fork]** をクリックして自身のアカウントにリポジトリを作成します。

### 2. キーマップの編集 (Keymap Customization)

リポジトリ内のファイルを編集して、好みのキー配列や動作を設定します。  
詳しい編集内容については [公式ドキュメント](https://zmk.dev/docs/keymaps) や有志の方の記事などを参考にしてください。

#### 物理レイアウト（physical-layout）の指定

`.keymap` ファイル冒頭にある `chosen` ノード内の `zmk,physical-layout` を、ご自身の使用するキーボードのキー数に合わせて変更してください。

```dts
/ {
    chosen {
        zmk,physical-layout = &layout40;
        // &layout20, &layout24, &layout30, &layout40, &layout48, &layout60;
    };
};
```

### 3. ファームウェアのビルドとダウンロード (Build & Download)

1. 変更をコミットして `main` ブランチに `git push`（または GitHub 上で直接編集・コミット）すると、自動的にビルドが開始されます。
2. **[Actions]** タブを開き、実行中のワークフロー（`Build Firmware`）を選択します。
3. ビルド完了後、画面下部の **Artifacts** セクションから `.uf2` ファイルを含む Zip をダウンロードします。

> [!NOTE]
> [skubmdi/zdmck](https://github.com/skubmdi/zdmck) でdevcontainerを使用したローカルビルドも可能です  
> Github Actionsでは数分かかるビルドも数秒で完了し、軽微な修正やデバッグが容易です。

---

### 4. キーボードへの書き込み (Flashing)

1. ダウンロードした Zip ファイルを解凍し、`.uf2` ファイルを取り出します（分割型の場合は左右それぞれのファイル）。
2. キーボード裏側のリセットボタンを2回素早く押し、ブートローダーモード（USBドライブとして認識される状態）にします。
3. 対応する `.uf2` ファイルを認識されたドライブにドラッグ＆ドロップして書き込みます。

> [!TIP]
> 左右分割の場合はuollp_left/uollp_right  
> 片手デバイスとして使用する場合はuollp を使用してください。
