WAI-ARIA
===

2018/10/03

Kobayashi Kazuhiro (kzhrk)

---

## WAI-ARIAとは

Webのコンテンツ（HTML Tag）に構造の関係性や振る舞い、状態に関する情報を定義できるプロパティ。  
アクセスビリティの向上、ダイバーシティな人々への補助を主な目的としている。

---

## ARIAで使用するプロパティ

48種類のプロパティが定義されている。  
[all aria-* attributes](https://www.w3.org/TR/wai-aria/#state_prop_def)

- aria-activedescendant
- aria-atomic
- aria-autocomplete
- aria-busy
- aria-checked
- aria-colcount
- aria-colindex
- aria-colspan
- aria-controls
- aria-current
- aria-describedby
- aria-details
- aria-disabled
- aria-dropeffect
- aria-errormessage
- aria-expanded
- aria-flowto
- aria-grabbed
- aria-haspopup
- aria-hidden
- aria-invalid
- aria-keyshortcuts
- aria-label
- aria-labelledby
- aria-level
- aria-live
- aria-modal
- aria-multiline
- aria-multiselectable
- aria-orientation
- aria-owns
- aria-placeholder
- aria-posinset
- aria-pressed
- aria-readonly
- aria-relevant
- aria-required
- aria-roledescription
- aria-rowcount
- aria-rowindex
- aria-rowspan
- aria-selected
- aria-setsize
- aria-sort
- aria-valuemax
- aria-valuemin
- aria-valuenow
- aria-valuetext

---

## roles

意味を持ったコンテンツのまとまりを定義するプロパティ。  
WAI-ARIA 1.1では81種類のroleが定義されている。  
[Definition of Roles](https://www.w3.org/TR/wai-aria/#role_definitions)

- alert
- alertdialog
- application
- article
- banner
- button
- cell
- checkbox
- columnheader
- combobox
- command
- complementary
- composite
- contentinfo
- definition
- dialog
- directory
- document
- feed
- figure
- form
- grid
- gridcell
- group
- heading
- img
- input
- landmark
- link
- list
- listbox
- listitem
- log
- main
- marquee
- math
- menu
- menubar
- menuitem
- menuitemcheckbox
- menuitemradio
- navigation
- none
- note
- option
- presentation
- progressbar
- radio
- radiogroup
- range
- region
- roletype
- row
- rowgroup
- rowheader
- scrollbar
- search
- searchbox
- section
- sectionhead
- select
- separator
- slider
- spinbutton
- status
- structure
- switch
- tab
- table
- tablist
- tabpanel
- term
- textbox
- timer
- toolbar
- tooltip
- tree
- treegrid
- treeitem
- widget
- window

---

## aria-*とrole

aria-*プロパティは特定のroleを持つ要素、または特定のroleを持つ要素の中で定義されなければならない。  
たとえば、[aria-checked](https://www.w3.org/TR/wai-aria/#aria-checked)はcheckbox, option, radio, switchのroleを持つ要素か、menuitemcheckbox, menuitemradio, treeitemを持つ要素を親に持つ場合に使用できる。

---

## JavaScriptとWAI-ARIA

ユーザのアクションで変更されるaria-*プロパティはJavaScriptで変更する必要がある。  
stateを表現するaria-checkedはcheckboxの変更で切り替わる。また、レスポンシブでレイアウトが変わる場合、表組みの順番を表す、aria-colindex, aria-colspan, aria-rowindex, aria-rowspanをwindowのresizeイベントで変更しなければならない。  
JavaScriptで利用できそうなaria-*プロパティを紹介していく。

### タブ

| role | description |
| :--- | :--- |
| [tablist](https://www.w3.org/TR/wai-aria/#tablist) | tab elementsのリスト |
| [tab](https://www.w3.org/TR/wai-aria/#tab) | tab |
| [tabpanel](https://www.w3.org/TR/wai-aria/#tabpanel) | tab elementと結びついたリソース |

| aria | value | description |
| :--- | :--- | :--- |
| [aria-orientation](https://www.w3.org/TR/wai-aria/#aria-orientation) | horizontal/undefined/vertical | 縦並びか横並びかの説明 |
| [aria-controls](https://www.w3.org/TR/wai-aria/#aria-controls) | ID reference list | 影響を与えるelementsのid |
| [aria-labelledby](https://www.w3.org/TR/wai-aria/#aria-labelledby) | ID reference list | elementが何からlabelされているかの説明 |

```html
<ul role="tablist" aria-orientation="horizontal">
  <li id="tab1" role="tab" aria-controls="tab1-contents">tab1</li>
  <li id="tab2" role="tab" aria-controls="tab2-contents">tab2</li>
  <li id="tab3" role="tab" aria-controls="tab3-contents">tab3</li>
  <li id="tab4" role="tab" aria-controls="tab4-contents">tab4</li>
</ul>
<div id="tab1-contents" role="tabpanel" aria-labelledby="tab1">tab1 contents</div>
<div id="tab2-contents" role="tabpanel" aria-labelledby="tab2">tab2 contents</div>
<div id="tab3-contents" role="tabpanel" aria-labelledby="tab3">tab3 contents</div>
<div id="tab4-contents" role="tabpanel" aria-labelledby="tab4">tab4 contents</div>
```

### モーダル

| role | description |
| :--- | :--- |
| [dialog](https://www.w3.org/TR/wai-aria/#dialog) |  |

| aria | value | description |
| :--- | :--- | :--- |
| [aria-modal](https://www.w3.org/TR/wai-aria/#aria-modal) | 	true/false | elementがmodalであることの説明 |
| [aria-labelledby](https://www.w3.org/TR/wai-aria/#aria-labelledby) | ID reference list | elementが何からlabelされているかの説明 |
| [aria-hidden](https://www.w3.org/TR/wai-aria/#aria-hidden) | true/false/undefined | elementが表示されているかの説明 |

```html
<button id="modal-open">モーダル1を開く</button>
<button id="modal-open2">モーダル2を開く</button>
<div class="overlay">
  <div role="dialog" aria-modal="true" aria-labelledby="modal-open modal-prev" aria-hidden="true">
    <p>モーダル1 コンテンツ</p>
    <button id="modal-next">Next</button>
  </div>
  <div role="dialog" aria-modal="true" aria-labelledby="modal-open2 modal-next" aria-hidden="true">
    <p>モーダル2 コンテンツ</p>
    <button id="modal-prev">Prev</button>
  </div>
</div>
```

### セレクト

| role | description |
| :--- | :--- |
| [list](https://www.w3.org/TR/wai-aria/#list) | listitemを含むelement |
| [listitem](https://www.w3.org/TR/wai-aria/#listitem) | listitem |

| aria | value | description |
| :--- | :--- | :--- |
| [aria-controls](https://www.w3.org/TR/wai-aria/#aria-controls) | ID reference list | 影響を与えるelementsのid |
| [aria-disabled](https://www.w3.org/TR/wai-aria/#aria-disabled) | true/false | elementが操作可能か |
| [aria-labelledby](https://www.w3.org/TR/wai-aria/#aria-labelledby) | ID reference list | elementが何からlabelされているかの説明 |
| [aria-hidden](https://www.w3.org/TR/wai-aria/#aria-hidden) | true/false/undefined | elementが表示されているかの説明 |

```html
<div>
  <select id="select" aria-controls="list" aria-disabled="false">
    <option value="option1">option1</option>
    <option value="option2">option2</option>
    <option value="option3">option3</option>
    <option value="option4">option4</option>
    <option value="option5">option5</option>
    <option value="option6">option6</option>
    <option value="option7">option7</option>
    <option value="option8">option8</option>
    <option value="option9">option9</option>
    <option value="option10">option10</option>
  </select>
  <ul id="list" role="list" aria-hidden="true" aria-labelledby="select">
    <li role="listitem">option1</li>
    <li role="listitem">option2</li>
    <li role="listitem">option3</li>
    <li role="listitem">option4</li>
    <li role="listitem">option5</li>
    <li role="listitem">option6</li>
    <li role="listitem">option7</li>
    <li role="listitem">option8</li>
    <li role="listitem">option9</li>
    <li role="listitem">option10</li>
  </ul>
</div>
```

### 非同期

| role | description |
| :--- | :--- |
| [button](https://www.w3.org/TR/wai-aria/#button) | ユーザのアクション（click or press）ができるelement |

| aria | value | description |
| :--- | :--- | :--- |
| [aria-disabled](https://www.w3.org/TR/wai-aria/#aria-disabled) | true/false | elementが操作可能か |
| [aria-busy](https://www.w3.org/TR/wai-aria/#aria-busy) | true/false | elementのコンテンツが更新中か |

```html
<button role="button" aria-disabled="false">Get Articles</button>
<article aria-busy="false">
</article>
<template>
  <section>
    <h1>{{title}}</h1>
    <p>{{contents}}</p>
  </section>
</template>
```

---

## なぜWAI-ARIAなのか

新しいWeb技術として注目されはじめている[Web Components](https://kzhrk-slide.github.io/web-components/#1)では、[Custom Elements](https://developer.mozilla.org/ja/docs/Web/Web_Components/Custom_Elements)によって独自タグを定義することになる。  
Custom Elementsで定義された要素はセマンティックな構造になりにくく、また検索エンジンのクローラに解釈されにくい。  
Web Componentsが一般化してくると、タグに対して意味付けを行うWAI-ARIAはマークアップする上で定義が必須なプロパティになってくる。

また、公共性の高いWebコンテンツでアクセスビリティを意識しないと、某ボランティア募集フォームのような扱いを受ける。  
**すべてのコンテンツはすべての人類に平等に配信されるべき**であり、そのためにはWAI-ARIAの適応はマークアップにおいて必須なのではないだろうか。
