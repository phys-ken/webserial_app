---

marp: true
header: 2022.1.24
footer: phys_ken

---

<!-- 
theme: gaia
size: 4:3
paginate: true
style: |
  section {

    background-color: #FFFFFF;
    font-family: 'Yu Gothic UI';
    color: black;

  }
-->


# エラー回避

<!-- headingDivider: 3 -->

<!-- _class: lead -->

## 測定値のエラー

* 距離センサーは、測定がうまくできないと[8890]を返す
  * 8mも測定できない（するつもりもない）
* ただし、webserial のグラフアプリに出力すると、グラフが読めなくなってしまう。
* どうすれば良いか？
* ヒント：条件分岐



## エラー回避
* もしエラーだったら
* そうじゃなかったら

## 測定値をなめらかにする
* 測定値の急な変化を抑える(ハイカットフィルター)

$$a = 0.1$$
$$x_{結果}=(1-a) \times x_{測定値} + a\times x_{ひとつ前の結果}$$

* $a$を微調整しながら、フィルター効果を実感しよう

## 速度のグラフを表示する
* 変数をうまく使おう
$$v = \frac{v_{now} - v_{pre}}{\Delta t}$$

* これをコードで書くと...?


<style type="text/css">

body {

  counter-reset: number 0; /* number のカウンタを 0 にセット */

}

h1 {

  position:relative; 
  padding:5px 20px; 
  font:bold  Arial, Helvetica, sans-serif; 
  color:#333; 
  background:#fff; 
  text-shadow:

    1px 1px 0 #fff,
    2px 2px 0 #999;

  border-top:#333 solid 3px; 
  border-bottom:#333 solid 3px; 

    background-image: -webkit-gradient(linear, left top, right bottom,
      from(			rgba(255, 255, 255, 0.0)), 
      color-stop(0.4, rgba(255, 255, 255, 0.0)), 
      color-stop(0.4, rgba(0, 0, 0, 0.1)), 
      color-stop(0.6, rgba(0, 0, 0, 0.1)), 
      color-stop(0.6, rgba(255, 255, 255, 0.0)),
      to(				rgba(255, 255, 255, 0.0))
      );

  background-image: -webkit-linear-gradient(top -45deg, 

      transparent 40%,
            rgba(0, 0, 0, 0.1) 40%,
            rgba(0, 0, 0, 0.1) 60%,
            transparent 60%
      );

  background-image: -moz-linear-gradient(top -45deg, 

      transparent 40%,
            rgba(0, 0, 0, 0.1) 40%,
            rgba(0, 0, 0, 0.1) 60%,
            transparent 60%
      );

  background-image: -o-linear-gradient(top -45deg, 

      transparent 40%,
            rgba(0, 0, 0, 0.1) 40%,
            rgba(0, 0, 0, 0.1) 60%,
            transparent 60%
      );

  background-image: linear-gradient(to bottom -45deg, 

      transparent 40%,
            rgba(0, 0, 0, 0.1) 40%,
            rgba(0, 0, 0, 0.1) 60%,
            transparent 60%
      );

  background-size:4px 4px; 

}
h1:before{

  content:" "; 
  position:absolute; 
  top:100%; 
  left:24px; 
  width:0; 
  height:0; 
  border-width:12px; 
  border-style:solid; 
  border-color:transparent; 
  border-top-color:#333; 

}
h1:after{

  content:" "; 
  position:absolute; 
  top:100%; 
  left:28px; 
  width:0; 
  height:0; 
  border-width:8px; 
  border-style:solid; 
  border-color:transparent; 
  border-top-color:#f0f0f0; 
  z-index:1; 

}

h2:before {

    counter-increment: number 1 ;

content: counter(number) "."; 

    height: 10px;
    width: 40px;
    left: 10px;
    position: absolute;
    top: 0px;

}

h2 {

    padding-bottom: 0.1em;

    position: relative;
    padding-left: 90px;
    margin-left: 10px;
      padding: 0em 2em;/*上下 左右の余白*/

  color: black; /*文字色*/
  background: transparent; /*背景透明に*/
  border-left: solid 5px black; /*左線*/
}

h3 {

    text-decoration: underline;

}

.kousiki {

    position: relative;
    margin: 2em 0;
    padding: 0.5em 1em;
    border: solid 3px black;
    border-radius: 8px;

}
.kousiki .box-title {

    position: absolute;
    display: inline-block;
    top: -13px;
    left: 10px;
    padding: 0 9px;
    line-height: 1;
    font-size: 19px;
    background: #FFF;
    color: black;
    font-weight: bold;

}
.kousiki p {

    margin: 0; 
    padding: 0;

}

</style>
