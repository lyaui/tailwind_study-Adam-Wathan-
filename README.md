# tailwind 
###### tags: `CSS` `Tailwind`
實作練習：
# Mike 環境設置教學
## 基礎環境安裝
[tailwind 官網](https://tailwindcss.com/docs/installation#using-tailwind-with-post-css)
[tailwindcss 超入門 - #1 安裝及使用](https://www.youtube.com/watch?v=0EoYARlGGW4)

1. 使用 Parcel 快速建立基本專案環境
![](https://i.imgur.com/l186Xdc.png =70%x)
2. `npm install tailwindcss` 安裝 Tailwind
3. `npm i  postcss-cli` 安裝 postcss
4. 在 src 中增加 `tailwindcss` 的資料夾與 `index.css` ，並導入相關必備指定檔案（postcss 會幫忙編譯）
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
5. `npx tailwindcss init` 進行初始化動作以建立 `tailwind.config.js`，該檔案可以用來客製化 CSS 的內容
6. 新增一個 `postcss.config.js` 檔案進行 tailwind 編譯與處理瀏覽器相容性問題
```javascript=
module.exports = {
  plugins: [
    // ...
    require('tailwindcss'), // 編譯 tailwind
    require('autoprefixer'), // 加上前綴字處理瀏覽器相容性問題
    // ...
  ]
}
```
7. 清除 `index.js` 中引入的 CSS ，並改成引入 `tailwindcss` 的  `index.css`
8. 使用 `npm run start` 就可以啟動專案看到樣式了

＊ 因為步驟 1 已設定好安裝，所以步驟 2, 3, 6可以跳過 


## 使用 PurgeCSS 幫檔案瘦身

[tailwind 檔案大小](https://tailwindcss.com/docs/controlling-file-size)

1. 安裝 PurgeCSS `npm install @fullhuman/postcss-purgecss --save-dev`
2. 依官網指令（上面網址內容）程式碼貼到`postcss.config.js` 中，在 bundle 時就會進行壓縮

## VScode套件安裝 & 客製化設定
### 相關套件安裝
1. 在 VScode 中安裝套件 Tailwind CSS IntelliSense，這樣打 class 就會出現相關建議
2. 進入設定調整 `tailwindCSS.emmetCompletions` 設為 true，開啟 emmet 功能

### 使用客製化設定
1. 將原本的 `tailwind.config.js` 檔案刪除，使用 `npx tailwindcss init --full` 語法，產生新的 `config` 設定檔。
2. 進入 config 檔中設定自訂顏色 aomidori

```sass=
colors: { aomidori: '#00AA90' }
```
3. 變更 config 檔後，記得刪除 cache 和 dist 檔，並執行 npm run start>，進入 html 檔後即可發現自定義的色彩。

![](https://i.imgur.com/jXqxRvN.png =70%x)
![](https://i.imgur.com/cIAkkeU.png =70%x)


---

# The Net Ninja 教學

[The Net Ninja](https://www.youtube.com/watch?v=bxmDnn7lrnk&list=PL4cUxeGkcC9gpXORlEHjc5bgnIi5HEGhw)

![](https://i.imgur.com/4qMhbHo.jpg =80%x)

## Intro & Setup（簡介、安裝）
![](https://i.imgur.com/q0MGIrL.png =60%x)
- 安裝 tailwind
先使用 `npm init` 建立 package.json
並使用 `npm install tailwindcss` 安裝 tailwind
![](https://i.imgur.com/gOeCdJY.png)
- 建立資料夾
分別建立src（編譯書寫）和public（輸出用）的資料夾
並新增 style.css 參考官方文件引入 tailwind 檔案
``` css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
- 編譯檔案
在 package.json 新增指令來編譯 tailwind ，之後執行 `npm run build-css` public 就會出現編譯好的 styles.css 檔案了

```
"build-css": "tailwindcss build src/styles.css -o public/styles.css"
```
![](https://i.imgur.com/jOVylHp.png)
（可以參考官方文件的寫法）

## Fonts & Colors（字型、色彩）
#### 字體大小 https://tailwindcss.com/docs/font-size
```
text-lg
text-2xl
text-6xl
```

#### 色彩 https://tailwindcss.com/docs/customizing-colors
```
text-yellow-400
text-gray-700
```

#### 字型大小寫
`uppercase`

#### 字體粗細
```
font-light 細
font-bold 粗
font-semibold 極粗
```


## Margin, Padding & Borders（空間相關）
#### margin 
https://tailwindcss.com/docs/margin
```
m-0 無
m-5 全局
mt-8 有方向
```
#### padding 
https://tailwindcss.com/docs/padding
```
p-0 無
p-5 全局
pt-8 有方向
```
#### border 
https://tailwindcss.com/docs/border-width
```
border-0 無
border 1px
border-b 底線1px
border-yellow-400 黃線
```
## Tailwind Config（新增自定義 class 樣式）
使用 `npx tailwindcss init --full` 產生 config 設定檔，`--full`即預設設定。

![](https://i.imgur.com/mKLiJnW.png)
在產生的 `tailwind.config.js` 中加入自定義的 font-size 
```
fontSize: {
  mammoth: '8rem',
},
```
然後執行之前設定的 `npm run build-css` 即會進行編譯，編譯完成後就可使用新增的 text-mammoth 了。

實作上不建議直接變更預設值檔案，會建議另外獨立新增檔案來放自己新增的值，這樣才能區分哪些是自己新增的哪些是系統預設，因此，將本來的 config 檔更名為`tailwind-default.config.js`來保留預設值（也可以不留，但就作為一個參考）。

之後重新執行 `npx tailwindcss init`（不用加- -full），會產生一支新的空白 `tailwind.config.js` 檔案，利用這個檔案來管理新增的 class 樣式。

新增主色與副色，然後執行 `npm run build-css` 重新編譯，就能使用自定義的色彩了。
![](https://i.imgur.com/vwCDOiu.png =50%x)

## Custom Fonts（自定義字型）
#### 使用內建字型
預設字型是 fontFamily 的 sans 系列，想用其他內建字型使用  `font-serif` 或 `font-mono` class

#### 引入外部字型（以 Google Fonts 為例）
選擇欲 Embed 的字型，選 @import 後將字串貼到 styles.css 中
![](https://i.imgur.com/D1fOXRk.png)
到 config 中新增 fontFamily，設定名為 body 字型為 Nunito 的class，編譯後就能使用`font-body`了。
![](https://i.imgur.com/ebwOirb.png =50%x)

## Using Flexbox
#### flex
https://tailwindcss.com/docs/flex
#### justify-center
https://tailwindcss.com/docs/justify-content
#### items-center
https://tailwindcss.com/docs/align-items#class-reference
## Responsive Classes（RWD 設定）
#### breakpoint https://tailwindcss.com/docs/breakpoints
斷點設計以 min-width 手機導向為基準，以下面設定為例：

預設一般狀況下 text 會是 green；
min-width 超過 640 會變 red；
min-width 超過 1024 會變 blue
```
text-green-500
sm:text-red-500  'sm': '640px'
lg:text-blue-500  'lg': '1024px'
```


## Cards
#### Border Radius 
https://tailwindcss.com/docs/border-radius
外框使用 overflow 修正圖片沒有圓角的狀況
#### width
https://tailwindcss.com/docs/width

#### Box Shadow
https://tailwindcss.com/docs/box-shadow
#### Object fit

https://tailwindcss.com/docs/object-fit#class-reference
圖片縮放呈現

![](https://i.imgur.com/Cqf4zhP.png =50%x)
```sass=
<div class="bg-white rounded overflow-hidden shadow-md">
  <img class="w-full h-32 sm:h-48 object-cover" src="img/stew.jpg" alt="stew" />
  <div class="m-4">
    <span class="font-bold">5 Bean Chilli Stew</span>
    <span class="block text-gray-500 text-sm">Recipe by Mario</span>
  </div>
</div>
```

## Badges
#### Position
https://tailwindcss.com/docs/position
![](https://i.imgur.com/vjGDqY7.png =50%x)

```
relative 父元素
absolute 子元素
top-0  top 位置
```
```sass=
<div class="bg-white rounded overflow-hidden shadow-md relative">

  ......
  
  <div class="bg-secondary-100 text-secondary-200 text-xs uppercase font-bold rounded-full p-2 absolute top-0 ml-2 mt-2">
    <span>25min</span>
  </div>
  
</div>
```
## @apply Directive
#### Extracting Components 
https://tailwindcss.com/docs/extracting-components
Tailwind 鼓勵我們使用 utility-first 的設計模式，然而一旦網站變得龐大，許多相同的卡片或樣式四處散落，重複的程式碼不僅冗長，修改時也很麻煩。

因此可以使用 `@apply` 語法，在 styles.css 檔案中建立自訂的 class 將樣式放在裡面，然後再用自訂的 class 取代原本一長串的 class，如此一來，碼程式碼會比較簡潔也能提高複用性。

這邊很推薦看文件，有更進階詳細的使用方法

![](https://i.imgur.com/ERDkJss.png)

```sass=
// card
<div class="card">
  <img class="w-full h-32 sm:h-48 object-cover" src="img/stew.jpg" alt="stew" />
  div class="m-4">
    <span class="font-bold">5 Bean Chilli Stew</span>
    <span class="block text-gray-500 text-sm">Recipe by Mario</span>
  </div>
  
  // badge
  <div class="badge">
    <span>25min</span>
  </div>
</div>
```
## Grids
#### Columns 欄數
在母元素設定
https://tailwindcss.com/docs/grid-template-columns
```
<div class="mt-8 grid lg:grid-cols-3 gap-10">

grid
grid-cols-3 每列三個
gap-10 cols 的間距
```

#### Columns span 跨多少欄
在子元素設定
https://tailwindcss.com/docs/grid-column#class-reference
```
<div class="grid md:grid-cols-3">     分 3 欄
  <div class="md:col-span-1"></div>   佔 1 欄
  <div class="md:col-span-2"></div>   佔 2 欄
</div>
```
## Buttons
建立按鈕的通用樣式
```
.btn {
    @apply rounded-full py-2 px-3 uppercase text-xs font-bold cursor-pointer tracking-wider
}

cursor-pointer 滑鼠反應
tracking-wider 字距
```
通用樣式 + 個別化樣式
```
<a href="#" class="btn border-primary md:border-2 text-primary">Login</a>
```
## Hover Effects
https://tailwindcss.com/docs/pseudo-class-variants
直接在要 hover 時顯現的效果前加上前綴 hover:，其他如 focus 的偽類同理
`hover:bg-primary`
## Transitions
transition
https://tailwindcss.com/docs/transition-property

```
transition     使用 transition 效果
ease-out       transition 的模式
duration-300   transition 的時間
```
# Adam Wathan 教學

[Adam Wathan](https://www.youtube.com/watch?v=21HuwjmuS7A&list=PL7CcGwsqRpSM3w9BT_21tUU8JN2SnyckR)

## Setting up Tailwind and PostCSS
### Tailwind, PostCSS 簡介
以下是安裝設定好的檔案，僅供參考。
https://github.com/lyaui/tailwind_Adam-Wathan_practice
__

Tailwind 是一款 PostCss 的 plugin，PostCSS 是一種後處理器（Postprocessors），利用 JS 插件將輸入的 CSS 轉成瀏覽器能懂的指令，並可依照需求進行客製化的引入，效能也較佳。

- 關於 PostCSS 的簡介可參考：[官方簡介](https://github.com/postcss/postcss/blob/HEAD/docs/README-cn.md)、[PostCSS](https://cythilya.github.io/2018/08/10/postcss/)
- SASS/ SCSS/ LESS 屬於預處理器(Preprocessors)，能將書寫的語法轉為 CSS 語法
- **一些環境已經支援 PostCSS，例如 laravel, Next.js, Vue cli，可以直接使用，不用再安裝 PostCSS**


### 安裝 Tailwind, PostCSS, autoprefixer
安裝 Tailwind 與 PostCSS（autoprefixer 處理瀏覽器前綴詞）
`$ npm install tailwindcss postcss-cli autoprefixer`

### 產生 Tailwind 設定檔
`$ npx tailwind init` 產生 `tailwind.config.js` 設定檔，可進行樣式客製化設定


### 產生 PostCSS 設定檔

依[官網](https://tailwindcss.com/docs/installation)指示，建立 postcss.config.js，並將下列程式碼貼到其中來引用 tailwind 和 autoprefixer，在 bundle 時就會進行壓縮。
``` javascript=
module.exports = {
  plugins: [
    // ...
    require('tailwindcss'),
    require('autoprefixer'),
    // ...
  ],
};
```
#### 引用 tailwind css 內容
建立一支 css/tailwind.css 的檔案，這支檔案之後會集中統一管理所有 css 檔案，在此先引入會用到的 tailwind 中的base/components/utilities
``` css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

#### 設定編譯指令

在 package.json 新增指令來編譯剛剛的 css/tailwind.css，之後執行 `npm run build-css` public 就會出現編譯好的 build/tailwind.css 檔案了。


- 沒有使用 PostCss 的設定
```
"build-css": "tailwindcss build css/tailwind.css -o public/build/tailwind.css"
```
- 使用 PostCss 的設定
```
"build-css": "postcss css/tailwind.css -o public/build/tailwind.css"
_____

＊執行`npm run build-css` 時可能會遇到下列issue，只要將 autoprefixer 降至 ^9.8.6 版本即可解決
https://github.com/parcel-bundler/parcel/issues/5160
```
![](https://i.imgur.com/YT3Kn7M.png =50%x)
（編譯後的資料夾狀態）

＊css/tailwind.css - 要編譯的 CSS 位置；
＊public/build/tailwind.css - 編譯好的檔案位置
＊可以參考官方文件的寫法

![](https://i.imgur.com/jOVylHp.png)

### 引用 css 到 html 中
在 public 建立 index.html 後，使用 link 語法引入編譯好的 build/tailwind.css 檔，之後就能吃到設定好的樣式了。
```
<link rel="stylesheet" href="build/tailwind.css" />
```

### VScode 相關套件安裝
1. 在 VScode 中安裝套件 Tailwind CSS IntelliSense，這樣打 class 就會出現相關建議
2. 進入設定調整 `tailwindCSS.emmetCompletions` 設為 true，開啟 emmet 功能

## The Utility-First Workflow
文件很詳細，依照需求好好查文件

## Responsive Design

tailwind 內建四種響應是尺寸

      sm: '640px',
      md: '768px',
      lg: '1024px',
      xl: '1280px',

inset
https://tailwindcss.com/docs/top-right-bottom-left
## Hover, Focus, and Active Styles

注意！不是所有行為都有設定反應，例如 hover 時字體變大、active 時背景色變更，此時就要在 `tailwind.config.js` 進行設定
```
  variants: {
  
  // 有順序性的
    backgroundColor: ['responsive', 'hover', 'focus', 'active'],
  },
```
結合運用
`md:hover:bg-green-400`
active-bg
https://tailwindcss.com/docs/configuring-variants

## Composing Utilities with @apply
建立可複用的 component class

```
// 樣式模組化前
<a href="#" class="inline-block px-5 py-3 shadow-lg rounded-lg bg-indigo-500 md:hover:bg-green-400 hover:bg-indigo-400 focus:outline-none focus:shadow-outline active:bg-indigo-600 text-white uppercase tracking-wider >Book your escape</a>

// 樣式模組化後
<a href="#" class="btn">Book your escape</a>
```

注意！@apply不支援前贅詞狀態的 class，例如：響應系列(sm:, md:, lg:),hover ,focus, active，等偽類要分開放（類似寫CSS），不然無法編譯。

全部放一起NG！！！

```
.btn {
    @apply inline-block px-5 py-3 shadow-lg rounded-lg bg-indigo-500 hover:bg-indigo-400 focus:outline-none focus:shadow-outline active:bg-indigo-600 text-white uppercase tracking-wider font-semibold text-sm sm:text-base
}
```

分門別類放 OK
``` sass
// btn 基礎樣式
.btn {
    @apply inline-block px-5 py-3 shadow-lg rounded-lg bg-indigo-500 text-white uppercase tracking-wider font-semibold text-sm
}

// 偽類
.btn:hover {
    @apply bg-indigo-400
}
.btn:focus {
    @apply outline-none shadow-outline;
}
.btn:active {
    @apply bg-indigo-600
}

// responsive
@screen sm {
    .btn {
        @apply text-base
    }
}
```

**注意事項！！！**
擺放順訊很重要，自定義的 component class 要放在 `@tailwind utilities` 上方，這樣新增的 utility class 才能覆蓋掉原本 btn 中的樣式，不然完全無法透過新增 utility class 的方式改變樣式。

``` sass
@tailwind base;
@tailwind components;

// 必須擺放在 utilities 上
.btn {
    @apply inline-block px-5 py-3 shadow-lg rounded-lg bg-indigo-500 text-white uppercase tracking-wider font-semibold text-sm
}

@tailwind utilities;
```
原本 btn 中設定 px-5，加上 utility class px-8 就可以蓋掉
```
<a href="#" class="btn px-8">Book your escape</a>
```


## Customizing Your Design System
建立預設所有class變數表作為參考用

`npx tailwind init tailwind-full.config.js --full`

直接放在theme會報錯，因為會整個覆蓋掉預設的tailwind檔案，因此要放在extend中進行擴充，而extend會和tailwind的預設值檔案進行合併
```
theme: {
    extend: {
      colors: {
        'brand-blue': '#1992d3',
      },
    },
  },
```

## Optimizing for Production with Purgecss

Tailwind 有爆多的 utility class，編譯後其實檔案不小，而使用 [PurgeCSS](https://purgecss.com/#sponsors-%F0%9F%A5%B0) 可以移除未使用到的樣式，為檔案進行瘦身。

(https://tailwindcss.com/docs/controlling-file-size#setting-up-purge-css-manually)
### 安裝 PurgeCSS
`npm install @fullhuman/postcss-purgecss --save-dev`

### 設定 config 檔

postcss.config.js
關於詳細設定可以參考[官方文件教學]

![](https://i.imgur.com/f41UJOn.png =70%x)

執行build後
before & after
![](https://i.imgur.com/GwSvAz4.png =50%x)![](https://i.imgur.com/hRnKVWD.png =50%x)




## Making Text Content Feel Designed
truncate
https://tailwindcss.com/docs/word-break
## Working with SVG Icons
https://tailwindcss.com/resources#icons
## Designing a Badge

## Cropping and Positioning Images

## Locking an Image to a Fixed Aspect Ratio

## Creating Depth with Shadows and Layers

## Building a Navbar Layout with Flexbox

## Toggling the Navbar Links on Mobile

## Making the Navbar Responsive

## Styling a Dropdown Menu

## Positioning the Dropdown Area

## Making the Dropdown Interactive

## Adapting the Dropdown for Mobile