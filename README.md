# ストップウォッチ/Stop Watch
## 使い方
1. [penguin-123456.github.io/stopwatch](https://penguin-123456.github.io/stopwatch)を開きます。
2. スタート/Startボタンを押してタイマーを開始します。
3. 止めるときは、ストップ/Stopを押します。
4. リセットするには、リセット/Resetを押します。
## 注意
- [こちら](https://tcd-theme.com/2021/08/javascript-countdowntimer.html)を参考にさせていただきました。
- バグがある場合は、[こちら](https://form.userlocal.jp/s/stopwatch-bug)からお知らせください。
## フォント・画像
- [Google Fonts](https://fonts.google.com)のRubikを使っています。
- ファビコンの画像は、Google Fontsから取ってきました。
## ソースコード
### index.html
~~~
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ストップウォッチ/Stop Watch</title>
    <link rel="icon" href="favicon.svg" type="image/svg">
    <meta name="description" content="ストップウォッチです。penguin-123456が作りました。">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>ストップウォッチ/Stop Watch</h1>
    <div id="container">
        <div id="time">00:00:00.000</div>
        <div id="buttons">
        <input id="start" type="button" value="スタート/Start">
        <input id="stop" type="button" value="ストップ/Stop">
        <input id="reset" type="button" value="リセット/Reset">
        </div>
    </div>  
    <script src="script.js"></script>
</body>
</html>
~~~
### style.css
~~~
@import url('https://fonts.googleapis.com/css2?family=Rubik&display=swap');
html,
body {
    font-size: 16px;
    background-color: #4285f4;
}

h1 {
    color: #ffffff;
    text-align: center;
    font-size: 2rem;
    margin: 3rem;
}

#container {
    background-color: #ffffff;
    width: 540px;
    border-radius: 1rem;
    margin: 0 auto;
    padding: 1.5rem;
    font-family: 'Rubik', sans-serif;
}

#time {
    color: #1e90ff;
    font-size: 3rem;
    text-align: center;
    padding: 1rem;
    border-radius: 1rem;
    box-shadow: 0 0 20px rgba(0, 139, 253, 0.25);
    margin: .5rem;
}

#buttons {
    font-size: 3rem;
    text-align: center;
}

#start,
#stop,
#reset {
    font-size: 1.5rem;
    border-radius: .3rem;
    box-shadow: 0 0 20px rgba(77, 78, 79, 0.25);
}
~~~
### script.js
~~~
const time = document.getElementById('time');
const startButton = document.getElementById('start');
const stopButton = document.getElementById('stop');
const resetButton = document.getElementById('reset');

// 開始時間
let startTime;
// 停止時間
let stopTime = 0;
// タイムアウトID
let timeoutID;

// 時間を表示する関数
function displayTime() {
  const currentTime = new Date(Date.now() - startTime + stopTime);
  const h = String(currentTime.getHours()-1).padStart(2, '0');
  const m = String(currentTime.getMinutes()).padStart(2, '0');
  const s = String(currentTime.getSeconds()).padStart(2, '0');
  const ms = String(currentTime.getMilliseconds()).padStart(3, '0');

  time.textContent = `${h}:${m}:${s}.${ms}`;
  timeoutID = setTimeout(displayTime, 10);
}

// スタートボタンがクリックされたら時間を進める
startButton.addEventListener('click', () => {
  startButton.disabled = true;
  stopButton.disabled = false;
  resetButton.disabled = true;
  startTime = Date.now();
  displayTime();
});

// ストップボタンがクリックされたら時間を止める
stopButton.addEventListener('click', function() {
  startButton.disabled = false;
  stopButton.disabled = true;
  resetButton.disabled = false;
  clearTimeout(timeoutID);
  stopTime += (Date.now() - startTime);
});

// リセットボタンがクリックされたら時間を0に戻す
resetButton.addEventListener('click', function() {
  startButton.disabled = false;
  stopButton.disabled = true;
  resetButton.disabled = true;
  time.textContent = '00:00:00.000';
  stopTime = 0;
});
~~~
