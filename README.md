English follows
# Power Apps UI Kit @Awaji

Power Apps キャンバスアプリ向けのプリビルドコントロール集です。YAML をコピーしてアプリに貼り付けるだけで、すぐに使えます。

---

## 📦 収録コントロール一覧

| コントロール | タイプ | 説明 |
|---|---|---|
| Success Toast | GroupContainer · AutoLayout | 操作完了を通知するトースト通知 |
| Header Bar | GroupContainer · AutoLayout | アイコン・タイトル・ユーザー情報を含むアプリヘッダー |
| Search Filter Bar | GroupContainer · ManualLayout | テキスト入力・ドロップダウン・日付ピッカー・ボタンを含む検索フィルター行 |
| Gallery Table | GroupContainer + Gallery | ヘッダー行・交互行・選択インジケーター付きのテーブル型ギャラリー |
| Tab Navigation | GroupContainer · Gallery | アクティブ下線付きの水平タブバー |
| Sidebar Navigation | GroupContainer · Gallery | アクティブハイライト・インジケーターバー付きの縦型サイドバーナビ |
| Icon Buttons | GroupContainer · ManualLayout | アイコン付きのソフトカラーボタン（保存 / 警告 / 詳細） |
| Input Controls | GroupContainer · ManualLayout | テキスト入力・コンボボックス・ドロップダウン・メモ・日付入力の5種類 |

---

## 🚀 使い方

### 1. UI Kit を開く

`canvaskit.html` をブラウザで開いてください。インストールやビルド作業は不要です。

### 2. テーマを選ぶ

各コントロールカードの右上にカラーパレットピッカーがあります。ドットをクリックしてテーマを切り替えてください：

- **Indigo** · **Emerald** · **Rose** · **Amber** · **Slate** · **Ocean**

プレビューと生成される YAML がリアルタイムで更新されます。

### 3. YAML をコピーする

コントロールカードの **Copy YAML** ボタンをクリックします。選択中のテーマの色が反映された YAML がクリップボードにコピーされます。

### 4. Power Apps に貼り付ける

1. **Power Apps Studio** でキャンバスアプリを開く
2. キャンバス上で **Ctrl + V**（Mac は **⌘ + V**）を押す

YAML が解析され、レイアウト・色・フォント・プロパティがすべて保持された状態でコントロールが挿入されます。

> **ヒント：** 貼り付けがうまくいかない場合は、上部メニューの **挿入 → クリップボードから貼り付け** をお試しください。

---

## 🎨 テーマシステム

すべてのコントロールは、1つの `primary` カラー値から自動計算されるカラーシステムを使用しています。

| トークン | 用途 | 計算方法 |
|---|---|---|
| `primary` | ボタン・アイコン・アクティブ状態 | テーマのベースカラー |
| `tint(p, 0.88)` | 入力・コンテナの背景 | primaryを白に近づけた色 |
| `shade(p, 0.20)` | テキスト・アイコンの色 | primaryを黒に近づけた色 |
| `tint(p, 0.55)` | ボーダー | 薄いprimaryのティント |
| `tint(p, 0.92)` | ホバー時の背景色 | 非常に薄いprimaryのティント |

色は Power Fx の `RGBA()` 式として出力されるため、アプリにそのまま使用できます。

---

## 📋 コントロールリファレンス

### Header Bar（ヘッダーバー）

```yaml
- conHeader_Slate:
    Control: GroupContainer@1.5.0
    Variant: AutoLayout
    Properties:
      Fill: =RGBA(235, 240, 245, 1)
      Height: =63
      LayoutAlignItems: =LayoutAlignItems.Center
      LayoutDirection: =LayoutDirection.Horizontal
      Width: =1287
```

**カスタマイズすべきプロパティ：**

| プロパティ | 変更内容 |
|---|---|
| `lblTitle_Slate > Text` | `"Power Apps Application"` をアプリ名に変更 |
| `icoApp_Slate > Icon` | `Icon.Camera` を任意のアイコンに変更 |
| `Fill` | ブランドカラーに合わせて変更 |

---

### Search Filter Bar（検索フィルターバー）

```yaml
- Container10_3:
    Control: GroupContainer@1.5.0
    Variant: ManualLayout
    Properties:
      Height: =96
      Width: =1320
```

**カスタマイズすべきプロパティ：**

| プロパティ | 変更内容 |
|---|---|
| `Label > Text` | フィールドラベルをデータに合わせて変更（例：`"会社名"`） |
| `Dropdown > Items` | データソースや選択肢リストに接続 |
| `DatePicker` | `SelectedDate` をフィルター変数に接続 |
| `btnSearch > OnSelect` | フィルターロジックを追加（例：`Set(varFilter, ...)`） |
| `btnClear > OnSelect` | フィルター変数をデフォルト値にリセット |

---

### Gallery Table（ギャラリーテーブル）

```yaml
- galleryTableLikecontainer_1:
    Control: GroupContainer@1.5.0
    Variant: ManualLayout
    Properties:
      Height: =405
      Width: =1366
```

**カスタマイズすべきプロパティ：**

| プロパティ | 変更内容 |
|---|---|
| `Gallery2_6 > Items` | データソースに接続（例：`Filter(MyTable, ...)`） |
| `cellName > Text` | `ThisItem.SampleHeading` を実際のフィールド名に変更（例：`ThisItem.CompanyName`） |
| `cellDate > Text` | 日付フィールドに変更 |
| `cellDetails > Text` | `ThisItem.SampleText` を詳細フィールドに変更 |
| `cellStatus > Text` | ステータスフィールドに変更 |
| `headerName > Text` | 列ヘッダーのラベルを更新 |

---

### Tab Navigation（タブナビゲーション）

```yaml
- navTabsContainer:
    Control: GroupContainer@1.5.0
    Variant: AutoLayout
```

**カスタマイズすべきプロパティ：**

| プロパティ | 変更内容 |
|---|---|
| `Gallery > Items` | `Table(...)` のタブ名とキーを更新 |
| `varSelectedTab` | `App.OnStart` でデフォルトのタブキーを初期化 |
| `OnSelect` | `varSelectedTab` を使ってコンテンツの表示/非表示を制御 |

---

### Sidebar Navigation（サイドバーナビゲーション）

```yaml
- navContainer_3:
    Control: GroupContainer@1.5.0
    Variant: AutoLayout
```

**カスタマイズすべきプロパティ：**

| プロパティ | 変更内容 |
|---|---|
| `GalleryNav_3 > Items` | ナビゲーション項目の名前・キー・アイコンを更新 |
| `navHeader_3 > Text` | `"PASONA"` をアプリ名または会社名に変更 |
| `varSelectedNav` | `App.OnStart` で初期化し、画面遷移に活用 |
| `OnSelect` | `Set(varSelectedNav, ...)` と共に `Navigate(...)` を追加 |

---

### Input Controls（入力コントロール）

すべての入力コントロールは同じコンテナパターンに従っています：

```yaml
- conInput_User:
    Control: GroupContainer@1.5.0
    Variant: ManualLayout
    Properties:
      Height: =40
      Width: =280
    Children:
      - icoUser:           # 先頭アイコン
      - txtInput_User:     # 実際の入力コントロール
```

**カスタマイズすべきプロパティ：**

| コントロール | 変更するプロパティ |
|---|---|
| TextInput | `HintText`・`Default`・`OnChange` |
| ComboBox | `Items`（データソースまたは選択肢リストに接続） |
| DropDown | `Items`・`OnChange` |
| メモ（複数行） | `HintText`・`Mode: TextMode.MultiLine` |
| DatePicker | `SelectedDate` を変数に接続 |

---

### Icon Buttons（アイコンボタン）

```yaml
- btnContainer_Mint_1:
    Control: GroupContainer@1.5.0
    Variant: ManualLayout
    Properties:
      Height: =50
      Width: =150
```

**カスタマイズすべきプロパティ：**

| プロパティ | 変更内容 |
|---|---|
| `btnMint_1 > Text` | ボタンラベルを変更（先頭のスペースはアイコンのオフセット用なので残してください） |
| `icoMint_1 > Icon` | 任意の `Icon.*` 値に変更 |
| `Fill` | コンテナの背景をカラーパレットに合わせて変更 |
| `btnMint_1 > OnSelect` | アクションロジックを追加 |

---

## 💡 活用のヒント

**データソースへの接続**

プレースホルダー `ThisItem.SampleHeading` / `ThisItem.SampleText` を、SharePoint リスト・Dataverse テーブル・コレクションの実際のフィールド名に置き換えてください：

```
ThisItem.SampleHeading  →  ThisItem.受注番号
ThisItem.SampleText     →  ThisItem.備考
```

**変数の初期化**

タブおよびサイドバーナビゲーションを動作させるために、`App.OnStart` に以下を追加してください：

```
Set(varSelectedTab, "HOME");
Set(varSelectedNav, "HOME");
```

**レスポンシブな幅の設定**

コントロールを画面幅に合わせて伸縮させるには、固定の `Width` 値を以下のように変更してください：

```
Width: =App.Width - 56
```

**ヘッダーの User() 関数について**

ヘッダーの `lblUser_Slate` は、Power Fx の数式でユーザー名を姓名の順に表示します：

```
=With( {
  fullName: Split(User().FullName, " ")
  },
  Last(fullName).Value & " " & First(fullName).Value
)
```

アプリが `User()` にアクセスできる環境であれば、設定不要で自動的に動作します。

---

## 🗂 ファイル構成

```
/
├── canvaskit.html      # UI Kit本体 — ブラウザで開く
├── README.md           # 英語版ドキュメント
└── README_JP.md        # 日本語版ドキュメント（このファイル）
```

---

## 📄 ライセンス

自由に使ってください
---

*Power Apps メーカーのために · @Awaji*









[README.md](https://github.com/user-attachments/files/26811683/README.md)
# Power Apps UI Kit @Awaji

A collection of prebuilt, themeable Power Apps canvas controls — ready to copy as YAML and paste directly into your app.

---

## 📦 What's Included

| Control | Type | Description |
|---|---|---|
| Success Toast | GroupContainer · AutoLayout | Dismissible success notification |
| Header Bar | GroupContainer · AutoLayout | App header with icon, title, and user info |
| Search Filter Bar | GroupContainer · ManualLayout | Filter row with text input, dropdowns, date pickers, and action buttons |
| Gallery Table | GroupContainer + Gallery | Table-like gallery with header row, alternating rows, and selection indicator |
| Tab Navigation | GroupContainer · Gallery | Horizontal tab bar with active underline indicator |
| Sidebar Navigation | GroupContainer · Gallery | Vertical sidebar nav with active highlight and indicator bar |
| Icon Buttons | GroupContainer · ManualLayout | Soft-color buttons with leading icon (Save / Alert / Details) |
| Input Controls | GroupContainer · ManualLayout | Text input, ComboBox, Dropdown, Memo, and Date input variants |

---

## 🚀 How to Use

### 1. Open the UI Kit

Open `canvaskit.html` in any modern browser. No installation or build step required.

### 2. Pick a Theme

Each control card has a color palette picker in the top-right corner. Click any dot to switch themes:

- **Indigo** · **Emerald** · **Rose** · **Amber** · **Slate** · **Ocean**

The preview and the generated YAML both update instantly.

### 3. Copy the YAML

Click **Copy YAML** on the control card. The YAML is copied to your clipboard, with all color values already reflecting your chosen theme.

### 4. Paste into Power Apps

1. Open your canvas app in **Power Apps Studio**
2. Press **Ctrl + V** (or **⌘ + V** on Mac) anywhere on the canvas

Power Apps will parse the YAML and insert the control — preserving layout, colors, fonts, and properties exactly as defined.

> **Tip:** If paste doesn't work, go to **Insert → Paste from clipboard** in the top menu.

---

## 🎨 Theming System

All controls use a shared color system derived from a single `primary` hex value. The kit automatically computes:

| Token | Usage | Derivation |
|---|---|---|
| `primary` | Buttons, icons, active states | Base theme color |
| `tint(p, 0.88)` | Input/container backgrounds | Primary mixed with white |
| `shade(p, 0.20)` | Text, icon colors | Primary mixed with black |
| `tint(p, 0.55)` | Borders | Light primary tint |
| `tint(p, 0.92)` | Hover fills | Very light primary tint |

Colors are output as Power Fx `RGBA()` expressions — ready to use directly in your app.

---

## 📋 Control Reference

### Header Bar

```yaml
- conHeader_Slate:
    Control: GroupContainer@1.5.0
    Variant: AutoLayout
    Properties:
      Fill: =RGBA(235, 240, 245, 1)
      Height: =63
      LayoutAlignItems: =LayoutAlignItems.Center
      LayoutDirection: =LayoutDirection.Horizontal
      Width: =1287
```

**Key properties to customize:**

| Property | What to change |
|---|---|
| `lblTitle_Slate > Text` | Replace `"Power Apps Application"` with your app name |
| `icoApp_Slate > Icon` | Replace `Icon.Camera` with your preferred icon |
| `Fill` | Update to match your brand color |

---

### Search Filter Bar

```yaml
- Container10_3:
    Control: GroupContainer@1.5.0
    Variant: ManualLayout
    Properties:
      Height: =96
      Width: =1320
```

**Key properties to customize:**

| Property | What to change |
|---|---|
| `Label > Text` | Replace field labels (e.g. `"会社名"`) with your column names |
| `Dropdown > Items` | Replace with your data source or choice list |
| `DatePicker` | Connect `SelectedDate` to your filter variables |
| `btnSearch > OnSelect` | Add your filter logic (e.g. `Set(varFilter, ...)`) |
| `btnClear > OnSelect` | Reset filter variables to defaults |

---

### Gallery Table

```yaml
- galleryTableLikecontainer_1:
    Control: GroupContainer@1.5.0
    Variant: ManualLayout
    Properties:
      Height: =405
      Width: =1366
```

**Key properties to customize:**

| Property | What to change |
|---|---|
| `Gallery2_6 > Items` | Replace with your data source (e.g. `Filter(MyTable, ...)`) |
| `cellName > Text` | Replace `ThisItem.SampleHeading` with your field (e.g. `ThisItem.CompanyName`) |
| `cellDate > Text` | Replace with your date field |
| `cellDetails > Text` | Replace `ThisItem.SampleText` with your detail field |
| `cellStatus > Text` | Replace with your status field |
| `headerName > Text` | Update column header labels |

---

### Tab Navigation

```yaml
- navTabsContainer:
    Control: GroupContainer@1.5.0
    Variant: AutoLayout
```

**Key properties to customize:**

| Property | What to change |
|---|---|
| `Gallery > Items` | Update the `Table(...)` with your tab names and keys |
| `varSelectedTab` | Initialize this variable in `App.OnStart` with your default tab key |
| `OnSelect` | The tab sets `varSelectedTab` — use this in your screen logic to show/hide content |

---

### Sidebar Navigation

```yaml
- navContainer_3:
    Control: GroupContainer@1.5.0
    Variant: AutoLayout
```

**Key properties to customize:**

| Property | What to change |
|---|---|
| `GalleryNav_3 > Items` | Update names, keys, and icons for your navigation items |
| `navHeader_3 > Text` | Replace `"PASONA"` with your app or company name |
| `varSelectedNav` | Initialize in `App.OnStart`; use it to drive screen navigation |
| `OnSelect` | Add `Navigate(...)` alongside `Set(varSelectedNav, ...)` |

---

### Input Controls

All input controls follow the same container pattern:

```yaml
- conInput_User:
    Control: GroupContainer@1.5.0
    Variant: ManualLayout
    Properties:
      Height: =40
      Width: =280
    Children:
      - icoUser:      # Leading icon
      - txtInput_User: # The actual input control
```

**Key properties to customize:**

| Control | Property to change |
|---|---|
| TextInput | `HintText`, `Default`, `OnChange` |
| ComboBox | `Items` (connect to your data source or choice list) |
| DropDown | `Items`, `OnChange` |
| Memo (MultiLine) | `HintText`, `Mode: TextMode.MultiLine` |
| DatePicker | Connect `SelectedDate` to a variable |

---

### Icon Buttons

```yaml
- btnContainer_Mint_1:
    Control: GroupContainer@1.5.0
    Variant: ManualLayout
    Properties:
      Height: =50
      Width: =150
```

**Key properties to customize:**

| Property | What to change |
|---|---|
| `btnMint_1 > Text` | Update button label (note: leading spaces create icon offset — keep them) |
| `icoMint_1 > Icon` | Replace with any `Icon.*` value |
| `Fill` | Change container background to match your palette |
| `btnMint_1 > OnSelect` | Add your action logic |

---

## 💡 Tips

**Connecting to a data source**

Replace `ThisItem.SampleHeading` / `ThisItem.SampleText` placeholders with real field names from your SharePoint list, Dataverse table, or collection:

```
ThisItem.SampleHeading  →  ThisItem.OrderNumber
ThisItem.SampleText     →  ThisItem.Remarks
```

**Initializing variables**

Add these to `App.OnStart` to support tab and sidebar navigation:

```
Set(varSelectedTab, "HOME");
Set(varSelectedNav, "HOME");
```

**Responsive width**

To make controls fill the screen width, replace fixed `Width` values with:

```
Width: =App.Width - 56
```

**Using User() in the Header**

The header's `lblUser_Slate` uses a Power Fx formula to display the user's name in Last First order:

```
=With( {
  fullName: Split(User().FullName, " ")
  },
  Last(fullName).Value & " " & First(fullName).Value
)
```

This works automatically — no configuration needed as long as the app has access to `User()`.

---

## 🗂 File Structure

```
/
├── canvaskit.html      # The UI Kit — open in browser
└── README.md           # This file
```

---

## 📄 License

MIT — free to use in personal and commercial Power Apps projects.

---

*Built for Power Apps makers · @Awaji*
