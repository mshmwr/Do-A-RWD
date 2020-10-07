# DAY1: RWD 框架，包含 HTML 和 CSS

## 基礎概念

### HTML5 語意標籤

HTML5 的最新規格中，提供了一系列語意標籤（Semantic Elements）。

以下幾對 HTML 標籤在版面顯示上是完全相同的:

```html
<div>Hello</div>
<header>Hello</header>
<main>Hello</main>
<footer>Hello</footer>
```

既然語意標籤和`<div>`有相同的排版特性，那為什麼要使用語意標籤呢？最大的目的，**是讓搜尋引擎或是其他軟體工具，可以更清楚的了解網頁中每個區塊的設計目的**。

引用:[ HTML5 語意標籤](https://training.pada-x.com/docs/article.jsp?key=html5-semantic-elements)

---

## 架構步驟

### 列出需要的區塊和 CSS ID

- CSS ID: 根據各網站需求不同而會有所變動

  - 語意標籤 `<header>`

    - top-head: 此處用法等同於`<nav>`，可以放選單、toogle

  - 語意標籤 `<section>`，根據網站內容而定

    - header
    - news
    - story
    - special
    - menu
    - goods
    - access

  - 語意標籤 `<footer>`
    - footer

### 幫區塊上色(CSS)

參考使用 css 語法

```css
@media screen and (max-width: 991px) #top-head {
  width: 100%;
  padding: 0;
  top: 0;
  position: fixed;
  margin-top: 0;
}

article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
  background-color: #eeefeb;
}

footer {
  background-color: #eeefeb;
  font-size: 14px;
}
```

### 次區塊與 RWD 應用

- 次區塊: 每一個區塊裡的小區塊，可能有 1~N 個。
- RWD: 對應銀幕尺寸縮放畫面中，小區塊(block)的內容。

#### 參考 bootstrap 4 的網格系統

- 認識畫面解析度、螢幕寬度和 css 名稱
  | 設備大小 | 解析度 | CSS | 螢幕寬度 |
  | :------------------ | :-----: | :------- | :------------------------ |
  | Extra small devices | <576px | .col- | width: auto (or no width) |
  | Small devices | ≥576px | .col-sm- | width: 540px |
  | Medium devices | ≥768px | .col-md- | width: 720px |
  | Large devices | ≥992px | .col-lg- | width: 960px |
  | Xlarge devices | ≥1200px | .col-xl- | width: 1140px |

  引用: [bootstrap 的版面規劃](http://dic.vbird.tw/webdesign/main2017/unit11.php)
  <br>

- bootstrap 的佈局示意圖
  ![](https://miro.medium.com/max/1350/1*RYhcfCsvsd8eeCzMLfu0Uw.png "bootstrap的佈局")

  <table><tr><td bgcolor=#DEDEDE>
    <font size=2>
    <b>計算bootstrap佈局的大小(以<u>.col-md-4</u>舉例)</b>：<br>
    螢幕大小為100%<br>
    切分成12格 (bootstrap最多分成12格)<br>
    所以一格的大小 = 100% / 12 ≒ 8%<br>
    因此 .col-md-4 的大小 = (100% / 12) * 4 = 33%
    </font>
  </td></tr></table>

  ```css
  /* 先做行與列的基礎設定 */
  .row {
    display: flex;
    flex-wrap: wrap;
  }
  .col {
    flex-grow: 1;
    margin: 15px;
  }
  ```

- RWD 應用(media query)

  - 對應銀幕尺寸來撰寫 CSS 的方法叫做`media query`。
    把上方佈局中的 sm / md / lg / xl 等等行為全部寫在對應的 media query 中。

  - 此處參考引用網站中的 media query 內容，並改寫成一般 CSS 版本。
    (只列出參考範本中較常使用到的 4,6,12，更詳細的 css 設定可去下載 bootstrap 檔案來使用。)

    ```css
    @media (max-width: 576px) {
      .col-4 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100% * 4 * 1 / 12);
        /*扣除 30px 源自於我們兩邊各自 margin 了 15px*/
      }
      .col-6 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100% * 6 * 1 / 12);
      }
      .col-12 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100%);
      }
    }

    @media (min-width: 576px) {
      .col-sm-4 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100% * 4 * 1 / 12);
        /*扣除 30px 源自於我們兩邊各自 margin 了 15px*/
      }
      .col-sm-6 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100% * 6 * 1 / 12);
      }
      .col-sm-12 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100%);
      }
    }

    @media (min-width: 768px) {
      .col-md-4 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100% * 4 * 1 / 12);
        /*扣除 30px 源自於我們兩邊各自 margin 了 15px*/
      }
      .col-md-6 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100% * 6 * 1 / 12);
      }
      .col-md-12 {
        flex-grow: 0;
        flex-basis: calc(-30px + 100%);
      }
    }
    ```

  - 其中把具有設定比例的 column 的 flex-grow 取消 (`flex-grow: 0;`)，是因為希望他只保持在我們計算出的對應比例下。
    - [更詳細了解 Flex 空間分配: flex-grow / flex-shrink / flex-basis](https://ithelp.ithome.com.tw/articles/10208741)

  引用: [40 行實作響應式的佈局系統-告訴你 col-sm-12-col-md-6-是如何實現](https://medium.com/@realdennis/40%E8%A1%8C%E5%AF%A6%E4%BD%9C%E9%9F%BF%E6%87%89%E5%BC%8F%E7%9A%84%E4%BD%88%E5%B1%80%E7%B3%BB%E7%B5%B1-%E5%91%8A%E8%A8%B4%E4%BD%A0col-sm-12-col-md-6-%E6%98%AF%E5%A6%82%E4%BD%95%E5%AF%A6%E7%8F%BE-4490a65b1a0)

- 實作(flexbox)

  - row 的 css 如下，要設定`display: flex;`
    ```css
    .row {
      display: flex; /*使用flexbox*/
      flex-wrap: wrap; /*超出範圍時是否換行的屬性*/
      justify-content: center; /*物件顯示置中*/
    }
    ```
  - container 中的 block 不會連在一起 & 空間分配

    ```css
    /*不會連在一起: 使用padding*/
    padding-right: 15px;
    padding-left: 15px;

    /* block的空間分配(2種)
       1. 設定 flex: 1; (依照設定比例分配剩餘空間)
       2. width: 40%; (設定固定寬度，搭配padding來調整畫面顯示大小)
    */

    /*實例*/
    .col-sm-6 {
      padding-right: 15px;
      padding-left: 15px;

      /*填滿剩餘空間*/
      /* flex: 1; */

      /*使用固定寬度*/
      width: 40%;

      min-height: 1px; /*設定網頁元素的最低高度限制*/
    }
    ```

- 心得

  - 排版：
    參考的網站使用 float 做排版，但是在參考網站設定(使用 float)進行實作的過程中，遇到排版會受到 float 寬高設定影響，導致排版亂掉的狀況。查了資料[^1]發現使用 float 要詳細設定各種高度，所以後來決定用前一個段落(RWD 應用)學到的 flex 來進行設定。
  - 兩種進行`media query`設定時，HTML 中設定套用 css 的方式：
    在進行`media query`設定時，寫在 HTML 中的 class`<div class="...">`有以下兩種寫法

    - 這裡使用的寫法是同一個 css class(`.col-sm-6`)，在不同螢幕寬度下有不同設定。
      ```html
      HTML:
      <div class="col-sm-6"></div>
      ```
      ```css
      css:
      /*為了方便觀看差異已簡化程式碼*/ @media (max-width: 768px) {
        .col-sm-6 {
          width: 80%; /*顯示單欄，80%*/
        }
      }
      @media (min-width: 768px) {
        .col-sm-6 {
          padding-right: 15px;
          padding-left: 15px;
          width: 40%; /*顯示兩欄，各40%*/
        }
      }
      ```
    - 前一個段落(RWD 應用)的範例，是在不同的螢幕寬度下，套用不同的 css

      ```html
      HTML:
      <div class="col-6 col-sm-6 col-md-6"></div>
      ```

      ```css
      @media (max-width: 576px) {
        .col-6 {
          flex-grow: 0;
          flex-basis: calc(-30px + 100% * 6 * 1 / 12);
        }
      }

      @media (min-width: 576px) {
        .col-sm-6 {
          flex-grow: 0;
          flex-basis: calc(-30px + 100% * 6 * 1 / 12);
        }
      }

      @media (min-width: 768px) {
        .col-md-6 {
          flex-grow: 0;
          flex-basis: calc(-30px + 100% * 6 * 1 / 12);
        }
      }
      ```

[^1]: [高度相同的排版解決方案](https://blog.kalan.dev/responsive-flex/)

# DAY2: 各欄位內容填充(CSS 套用)

將參考網站的 CSS 套用在對應的 HTML 上。
大多數 css 設定都可以直接使用，但會發現放入的資料內容會有不少地方出現顯示錯誤，或是出現不如預期的顯示，那是因為部分 class name 是使用 javascript 來製作畫面的動態效果。

## 實作

### CSS 的 RWD

一些 CSS 設定會在不同螢幕大小下顯示不同的內容，所以要去拉動螢幕，才能看到相對應的 CSS 內容。

### 超連結和 hover 設定

還沒做 XD

### 網站圖片

使用了 chrome 的擴充功能下載全部圖片。

## 結論

到這邊一個很基礎的沒有任何動態效果的 RWD 網站就完成了。
接下來為了更接近參考網站一點，要開始進入到 javascript 的階段了。

# DAY3~DAY5: 各欄位內容填充(動態效果):使用 javascript

DAY2 之前都是 HTML 和 CSS 語法可以處理的範圍，從 DAY3 開始，要加入 javascript 來實作啦。

## 01-圖片左右滑動(slick)

這個部分是看網路上關於 slick 的教學，做一個效果沒有那麼華麗的簡易版。因為直接套用網站的 HTML 程式碼會有數不盡的 bug 要解(實力不夠短時間解不了 orz)。
bug 的主要原因是 data-lazy(延遲載入圖片)，還有主程式使用的.js 檔的內容。直接複製主程式使用的.js 檔會噴一堆錯誤，所以還是按部就班乖乖自己寫。

### 實作

- 參考網站

  [slick 作者的 github](https://github.com/kenwheeler/slick): 總之有神先拜

  [Slick.js 使用方法](https://blog.csdn.net/cddcj/article/details/52172863): 參考的教學網站
  網站(Slick.js 使用方法)中是下載 css 檔和 js 檔來使用:

  ```
  slick.css
  slick.min.js
  ```

- 實作過程

  - 最簡易版 slick

    ```html
    <!-- 使用slick -->
    <link rel="stylesheet" href="../js/slick/slick-theme.css" />
    <link rel="stylesheet" href="../js/slick/slick.css" />

    <script type="text/javascript" src="../js/slick/slick.min.js"></script>
    ```

  - 換成作者提供的網址

    - js 檔要放在 body 內: WHY??

  - CSS 版型套用(熟悉的步驟)
  - data-lazy(延遲載入圖片)

### 心得

根據教學網站實作，但在寫 jQuery 使用到`.slick`時，會出現`Property 'slick' does not exist on type 'JQuery<HTMLElement>'`。
先講結論: 無視就好，還是可以用。

接下來是得到結論之前，曲折離奇的奇怪解法。不要學，這裡只是記錄下來而已，搞不好以後就會想通怎麼會這樣了，~~到時候再來解 bug~~。

- 在網路上找到的[解法](https://stackoverflow.com/questions/52156625/property-slick-does-not-exist-on-type-jqueryhtmlelement)，但我怎麼試怎麼錯(沒辦法宣告 declare)，雖然跑去 TypeScript 新增了一行`var $: any;`之後，的確沒有跳出錯誤通知，但我想這不會是正確的解法，後來還是刪掉了。

### style

使用了 OOO.js
style=""，style="..."在縮放時會出現

### 使 block 高度相等(js-matchHeigtht)

使用了 OOO.js

### 彈出式視窗(remodal)

npm
使用了 OOO.js

### 字型

要下載 font 檔。

### 其它

#### Role

[HTML 中的 role 属性](https://blog.csdn.net/annip/article/details/53455226)
