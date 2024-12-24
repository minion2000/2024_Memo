# Markdown エディタの WEB アプリ開発メモ

以下は、マークダウンエディタの Web アプリを作成するためのシンプルな例をステップごとに示します。以下のコードをコピーして実行することで、基本的なマークダウンエディタを動作させることができます。

---

### **1. 開発環境の準備**

1. Node.js をインストールしていない場合は、[公式サイト](https://nodejs.org/)からインストールします。
2. プロジェクトディレクトリを作成します。
   ```bash
   mkdir markdown-editor
   cd markdown-editor
   ```
3. プロジェクトを初期化します。
   ```bash
   npm init -y
   ```
4. 必要なパッケージをインストールします。
   ```bash
   npm install react react-dom marked vite
   ```

---

### **2. プロジェクト構成**

ディレクトリ構成は以下のようになります。

```
markdown-editor/
├── node_modules/
├── public/
│   └── index.html
├── src/
│   ├── App.jsx
│   ├── main.jsx
│   └── styles.css
├── package.json
├── vite.config.js
└── README.md
```

---

### **3. コードの作成**

#### **3.1 Vite 用の設定**

`vite.config.js` ファイルを作成します。

```javascript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
});
```

#### **3.2 HTML テンプレート**

`public/index.html` を作成します。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Markdown Editor</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

#### **3.3 React のエントリーポイント**

`src/main.jsx` を作成します。

```javascript
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import "./styles.css";

ReactDOM.createRoot(document.getElementById("root")).render(<App />);
```

#### **3.4 Markdown エディタのロジック**

`src/App.jsx` を作成します。

```javascript
import React, { useState } from "react";
import { marked } from "marked";

const App = () => {
  const [markdown, setMarkdown] = useState("");

  const handleInputChange = (e) => {
    setMarkdown(e.target.value);
  };

  return (
    <div className="app">
      <textarea
        className="editor"
        value={markdown}
        onChange={handleInputChange}
        placeholder="Type your markdown here..."
      />
      <div
        className="preview"
        dangerouslySetInnerHTML={{ __html: marked(markdown) }}
      ></div>
    </div>
  );
};

export default App;
```

#### **3.5 スタイルの追加**

`src/styles.css` を作成します。

```css
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f4f4f4;
}

.app {
  display: flex;
  width: 90%;
  max-width: 1200px;
  height: 80%;
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.editor {
  width: 50%;
  padding: 10px;
  font-size: 16px;
  border: none;
  outline: none;
  resize: none;
}

.preview {
  width: 50%;
  padding: 10px;
  overflow-y: auto;
  background: #fafafa;
  border-left: 1px solid #ddd;
}
```

---

### **4. 開発サーバーの起動**

1. 開発サーバーを起動します。
   ```bash
   npx vite
   ```
2. ブラウザで `http://localhost:5173` を開きます。

---

### **5. 完成したアプリの動作**

- 左側のテキストエリアに Markdown を入力すると、右側にリアルタイムで HTML に変換されたプレビューが表示されます。
- 例えば、以下の Markdown を入力すると:

  ```markdown
  # Hello World

  - This is a list item
  - **Bold text**
  - _Italic text_
  ```

  プレビューには以下が表示されます:

  # Hello World

  - This is a list item
  - **Bold text**
  - _Italic text_

---

### **6. 拡張アイデア**

1. **コードブロックのハイライト**:

   - `highlight.js`を導入してコードのシンタックスハイライトを実装。
     ```bash
     npm install highlight.js
     ```

2. **ダークモード**:

   - ボタンでテーマを切り替えられるようにする。

3. **保存機能**:

   - ローカルストレージを利用して Markdown を保存。

4. **ファイルのインポート/エクスポート**:
   - ファイルのアップロードやダウンロード機能を追加。

---

これで、基本的な Markdown エディタが完成します。拡張機能を追加してさらに便利なツールに進化させてください！
