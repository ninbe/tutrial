# 5 日目

# React 入門

ライブラリを使った Web アプリケーション開発

---

# ゴール

### 5 日目代表的なライブラリである React の基本的な概念を理解し、

### 簡単な Web アプリケーションを作成できるようになる。

---

# アジェンダ

- **React について**
  - React とは、コンポーネント指向、SPA
- **React の環境構築**
  - Create React App を使ったプロジェクトの作成
- **React の基本**
  - ルート要素、エントリーポイント
  - JSX
  - Props と State、フック

---

# React とは

- ユーザーインターフェース (UI) を構築するための フレームワーク
- Meta(旧 Facebook) によって開発され、2013 年にオープンソース化
- ページを構成する部品を作成し、それらを組み合わせて UI を構築する
  - **コンポーネント指向**
- **SPA (Single Page Application)** の開発に適している

---

# コンポーネント指向

##### 独立した再利用可能な部品である「コンポーネント」を組み合わせて、システムを構築する考え方

- React ではコンポーネントを組み合わせて UI を構築する

![Videoコンポーネント](image-1.png)

---

# SPA (Single Page Application)

#### 初回ページ表示後は新しいページを読み込まず、JavaScript を使ってページの一部だけを更新するアプリケーション

<br>

- ページ遷移が高速で、ユーザー体験が向上する
- 反対語は MPA(Multi Page Application)
  - ページ遷移ごとに新しいページを読み込むアプリケーション

---

# React プロジェクトの作成

- React を使用した開発の始め方にはいくつかの方法がある
  - [react.dev - Start a New React Project](https://react.dev/learn/start-a-new-react-project)
- 今回はシンプルな Create React App を使用してプロジェクトを作成する
  - プロジェクト名は`first-react-app`とする
    <br>

```shell
npx create-react-app first-react-app
```

※npx の実行には npm の環境設定が必要

---

# React プロジェクトの内容

- Create React App で作成されたプロジェクトは以下のような構成になっている
  - 主要なファイルを記載

```
first-react-app
├── node_modules      - プロジェクトで使用するライブラリ一式
├── package.json      - パッケージ情報
├── public
│   └── index.html    - トップページ
└── src
    ├── App.css       - Appコンポーネントのスタイル
    ├── App.js        - Appコンポーネント
    ├── App.test.js   - Appコンポーネントのテストコード
    ├── index.css     - アプリ共通のスタイル
    ├── index.js      - アプリのエントリーポイント(起動ファイル)
    └── logo.svg      - ロゴ画像
```

---

# React プロジェクトの起動

```shell
cd first-react-app
npm start
```

- コマンドが成功したらブラウザで http://localhost:3000/ にアクセスする
- 以下の画面が表示されれば成功です

![w:350 alt text](image-3.png)

---

# npm start は何をしているか

- `npm start` コマンドは `package.json` に記述された `start` スクリプトを実行している
- `package.json` の `scripts` セクションには、プロジェクトで使用できるスクリプトが定義されている

```json
// package.jsonの一部

{
  "scripts": {
    "start": "react-scripts start" // npm start で実行されるコマンド
  }
}
```

---

# ページが表示されるまでの流れ

1. React アプリケーションの [URL](http://localhost:3000) にアクセスする
2. ブラウザが `index.html` を読み込み `<div id="root"></div>` が検出される
   -> **ルート要素**
3. `index.js` が読み込まれ `id="root"` の要素に対して App コンポーネント(`App.js`)が埋め込まれる
   -> **エントリーポイント**
4. App コンポーネント(`App.js`)が表示され、アプリケーションを操作できるようになる

---

# ルート要素

- React アプリケーションを反映するための場所
- 今回の例では `index.html` の `<div id="root"></div>` がルート要素

---

# エントリーポイント

- React アプリケーションで最初に呼び出されるファイル
- 今回の例では `index.js` がエントリーポイント

---

# 演習

- 「Hello World!」と表示させる

![w:400 text](image-4.png)

---

# 回答例

```javascript
// App.js

import logo from "./logo.svg";
import "./App.css";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>Hello World!</p>
      </header>
    </div>
  );
}

export default App;
```

---

# 演習

- 背景色を白にする
- 「Hello World!」を赤文字にする

![w:300](image-5.png)

---

# 回答例

```css
/* App.css */

.App-header {
  background-color: #ffffff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: rgb(255, 0, 0);
}
```

---

# JSX とは

- React で使われる JavaScript の構文拡張
- JavaScript の中に HTML のようなマークアップを記述できる
- `App.js`は JSX で記述されている

---

# JSX の基本ルール

- 単一のルート要素を持つ必要がある
- 自己終了タグは `<タグ名 />` で記述する
- JavaScript の式を `{}` で囲むことで埋め込むことができる
- HTML の属性を指定する別名が存在する

---

# 単一のルート要素を持つ必要がある

```javascript
// NG: 複数のルート要素があるためエラー
return (
  <p>Hello</p>
  <p>World!</p>
);

// OK: div 要素で囲むことで単一のルート要素となる
return (
  <div>
    <p>Hello</p>
    <p>World!</p>
  </div>
);
```

---

# 自己終了タグは `<タグ名 />` で記述する

- 子要素をもたない要素は自己終了タグを使用する

```javascript
// NG: 自己終了タグがない
<img src={logo} alt="logo">

// OK: 自己終了タグがある
<img src={logo} alt="logo" />
```

---

# JavaScript の式を `{}` で囲むことで埋め込むことができる

```javascript
const name = "SHIFT";
return (
  // name の値が埋め込まれる
  <h1>Hello, {name}!</h1>
);
```

---

# HTML の属性を指定する別名が存在する

```javascript
return (
  // HTML の class 属性は className として記述する
  <div className="App">
    // onclick 属性 は onClick として記述する
    <button onClick={handleClick}>Click me</button>
  </div>
);
```

---

# 演習

- ボタンコンポーネント(JSX)を作成して、トップページにボタンを表示させる

---

# 回答例

- Button.js を作成

```javascript
// Button.js

function Button() {
  return (
    <div>
      <button>Click me</button>
    </div>
  );
}

export default Button;
```

---

- App.js に Button コンポーネントを追加

```javascript
import logo from "./logo.svg";
import "./App.css";
import Button from "./Button"; // Button コンポーネントをインポート

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>Hello World!</p>
        <Button /> // Button コンポーネントを配置
      </header>
    </div>
  );
}

export default App;
```

---

# Props と State

- コンポーネントで値を扱うための仕組み
- Props
  - コンポーネントに値を渡すための仕組み
- State
  - コンポーネント内の状態を管理する仕組み
- Props で値をうけとり、State で状態を管理するのが基本的な使い方

---

# Props の基本

- Props として `name` を受け取り、`Hello {name}!` と表示する Welcome コンポーネント
- Props を渡すコンポーネントで `name` という名前を指定して値を渡す
- 受け取った Props は Props.名前 の形式でアクセスできる
- Props は読み取り専用で、コンポーネント内で変更することはできない

```javascript
// Props を受け取るコンポーネント
function Welcome(props) {
  return <div>Hello {props.name}!</div>;
}

// Props を渡すコンポーネント
function App() {
  return <Welcome name="SHIFT" />;
}
```

---

# State の基本

- State の値は useStage 関数を使って初期化する
- State の値を格納する変数 A と、その値を更新する関数 B を定義する

```javascript
import { useState } from "react";

function ClickButton() {
  const [clickState, setClick] = useState("してない"); // 初期値は"してない"
  const handleClick = () => {
    setClick("した"); // ボタンがクリックされたら"した"に更新
  };
  return <button onClick={handleClick}>クリックした？: {clickState}</button>; // Stateの値(clickState)を表示
}
```

---

# useState 関数

- コンポーネントの情報を管理するための関数
- useState 関数は 2 つの要素を持つ配列を返す
  - 1 つ目の要素: State の値
  - 2 つ目の要素: State の値を更新する関数
- 「フック」と呼ばれるコンポーネントに機能を追加する仕組みの 1 つ
- `use` で始まる関数はフック
  - 他には useEffect、useRef など

---

# 演習

Props と State を使って、ボタンをクリックするとカウントアップするアプリケーションを作成する

- 初期値は Prop を使って渡された値を使用する
- State を使って渡された値を管理し、ボタンをクリックするとカウントアップする

---

# 回答例

```jsx
// Counter.js
import { useState } from "react";

export default function Counter(props) {
  const [count, setCount] = useState(props.initialCount); // 初期値を Props から受け取る
  return (
    <div>
      <p>{count} 回クリックされました</p> // props で受け取った値を管理して表示
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

// App.js
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <Counter initialCount={0} /> // 初期値を 0 で渡す
      </header>
    </div>
  );
}
```

---

# 5 日間の研修を終えて

### 言語研修「JavaScript/TypeScript + React」お疲れ様でした！

---

# 5 日間の研修を終えて

初日に掲げたゴール
**「JavaScript/TypeScript の基礎を理解し、
基本的な Web アプリケーション開発の一歩目を踏み出す」**
は達成できましたか？

短い期間ではありましたが皆さんが真剣に取り組み、
多くの知識と技術を身につけられたと思います。

---

# 今後に向けて

---

# 学習の参考サイト

- [MDN - JavaScript](https://developer.mozilla.org/ja/docs/Web/JavaScript)

- [React 公式ドキュメント](https://ja.react.dev/)

---
