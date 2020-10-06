# DAY1: RWD框架，包含HTML和CSS

## 基礎概念
### HTML5語意標籤

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

***
## 架構步驟
### 列出需要的區塊和CSS ID
* CSS ID: 根據各網站需求不同而會有所變動
  
  * 語意標籤 `<header>`
    * top-head: 此處用法等同於`<nav>`，可以放選單、toogle

  * 語意標籤 `<section>`，根據網站內容而定
    * header
    * news
    * story
    * special
    * menu
    * goods
    * access

  * 語意標籤 `<footer>`
    * footer

### 幫區塊上色(CSS)
參考使用css語法
```css
@media screen and (max-width: 991px)
#top-head {
    width: 100%;
    padding: 0;
    top: 0;
    position: fixed;
    margin-top: 0;
}

article, aside, details, figcaption, figure, footer, header, hgroup, main, menu, nav, section, summary {
    display: block;
    background-color: #eeefeb;
}

footer {
    background-color: #eeefeb;
    font-size: 14px;
}
```
### 次區塊與RWD應用
- 次區塊: 每一個區塊裡的小區塊，可能有1~N個。
- RWD: 對應銀幕尺寸縮放畫面中，小區塊(block)的內容。
#### 參考bootstrap 4 的網格系統
- 認識畫面解析度、螢幕寬度和css名稱
  | 設備大小            | 解析度  | CSS      | 螢幕寬度                  |
  | :------------------ | :-----: | :------- | :------------------------ |
  | Extra small devices | <576px  | .col-    | width: auto (or no width) |
  | Small devices       | ≥576px  | .col-sm- | width: 540px              |
  | Medium devices      | ≥768px  | .col-md- | width: 720px              |
  | Large devices       | ≥992px  | .col-lg- | width: 960px              |
  | Xlarge devices      | ≥1200px | .col-xl- | width: 1140px             |

  引用: [bootstrap的版面規劃](http://dic.vbird.tw/webdesign/main2017/unit11.php)
<br>
- bootstrap的佈局示意圖
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

  
- RWD應用(media query)
  - 對應銀幕尺寸來撰寫 CSS 的方法叫做`media query`。
    把上方佈局中的 sm / md / lg / xl 等等行為全部寫在對應的media query中。
  
  - 此處參考引用網站中的media query內容，並改寫成一般CSS版本。
    (只列出參考範本中較常使用到的4,6,12，更詳細的css設定可去下載bootstrap檔案來使用。)
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


  引用: [40行實作響應式的佈局系統-告訴你col-sm-12-col-md-6-是如何實現](https://medium.com/@realdennis/40%E8%A1%8C%E5%AF%A6%E4%BD%9C%E9%9F%BF%E6%87%89%E5%BC%8F%E7%9A%84%E4%BD%88%E5%B1%80%E7%B3%BB%E7%B5%B1-%E5%91%8A%E8%A8%B4%E4%BD%A0col-sm-12-col-md-6-%E6%98%AF%E5%A6%82%E4%BD%95%E5%AF%A6%E7%8F%BE-4490a65b1a0) 


- 實作(flexbox)
  
  - row的css如下，要設定`display: flex;`
    ```css
    .row {
      display: flex; /*使用flexbox*/
      flex-wrap: wrap; /*超出範圍時是否換行的屬性*/
      justify-content: center; /*物件顯示置中*/
    }
    ```
    
  - container中的block不會連在一起 & 空間分配
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
    參考的網站使用float做排版，但是在參考網站設定(使用float)進行實作的過程中，遇到排版會受到float寬高設定影響，導致排版亂掉的狀況。查了資料[^1]發現使用float要詳細設定各種高度，所以後來決定用前一個段落(RWD應用)學到的flex來進行設定。
  - 兩種進行`media query`設定時，HTML中設定套用css的方式：
    在進行`media query`設定時，寫在HTML中的class`<div class="...">`有以下兩種寫法
    - 這裡使用的寫法是同一個css class(`.col-sm-6`)，在不同螢幕寬度下有不同設定。
      ```html
      HTML:
      <div class="col-sm-6"></div>
      ```
      ```css
      CSS:
      /*為了方便觀看差異已簡化程式碼*/
      @media (max-width: 768px) { 
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
    - 前一個段落(RWD應用)的範例，是在不同的螢幕寬度下，套用不同的css
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

# DAY2: 各欄位內容填充(CSS套用)
將參考網站的CSS套用在對應的HTML上。
大多數css設定都可以直接使用，但會發現放入的資料內容會有不少地方出現顯示錯誤，或是出現不如預期的顯示，那是因為部分class name是使用javascript來製作畫面的動態效果。

## 實作
### CSS的RWD
一些CSS設定會在不同螢幕大小下顯示不同的內容，所以要去拉動螢幕，才能看到相對應的CSS內容。
### 超連結和hover設定
還沒做XD
### 網站圖片
使用了chrome的擴充功能下載全部圖片。

## 結論
到這邊一個很基礎的沒有任何動態效果的RWD網站就完成了。
接下來為了更接近參考網站一點，要開始進入到javascript的階段了。

# DAY3~DAY5: 各欄位內容填充(動態效果):使用javascript
DAY2之前都是HTML和CSS語法可以處理的範圍，從DAY3開始，要加入javascript來實作啦。
## 01-圖片左右滑動(slick)
這個部分是看網路上關於slick的教學，做一個效果沒有那麼華麗的簡易版。因為直接套用網站的HTML程式碼會有數不盡的bug要解(實力不夠沒辦法一眼看出哪些地方缺了什麼東西要補orz)。
### 實作
[slick作者的github](https://github.com/kenwheeler/slick): 總之有神先拜
[Slick.js使用方法](https://blog.csdn.net/cddcj/article/details/52172863): 參考的教學網站
網站(Slick.js使用方法)中是下載css檔和js檔來使用:
```
slick.css
slick.min.js
```

- js檔要放在body內: WHY??
- data-lazy(延遲載入圖片)





### style
使用了OOO.js
style=""，style="..."在縮放時會出現
### 使block高度相等(js-matchHeigtht)
使用了OOO.js
### 彈出式視窗(remodal)
npm
使用了OOO.js
### 字型
要下載font檔。

### 其它
#### Role
[HTML中的role属性](https://blog.csdn.net/annip/article/details/53455226)