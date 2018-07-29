### 자바스크립트 - xhr을 이용한 http 메소드 호출

프록시 툴을 사용하지 못할 때, 서버에 직접 올려 사용한다.

<pre><code>

＜div id="optdiv">응답에 Allow 헤더가 있으면 출력됨＜/div>

＜script>
var data = null;
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;
xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
	document.getElementById("optdiv").innerHTML=this.getResponseHeader("Allow");
    console.log(this.responseText);
  }
});
xhr.open("OPTIONS", "https://www.xxx.co.kr/");
xhr.setRequestHeader("save-data", "on");
xhr.setRequestHeader("upgrade-insecure-requests", "1");
xhr.setRequestHeader("user-agent", "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36");
xhr.setRequestHeader("accept", "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8");
xhr.setRequestHeader("accept-encoding", "gzip, deflate, br");
xhr.setRequestHeader("accept-language", "ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7");
xhr.setRequestHeader("cache-control", "no-cache");
xhr.send(data);
＜/script>

</code></pre>

### 자바스크립트 - jquery ajax를 이용한 http 메소드 호출

<pre><code>

＜script src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js">＜/script>
＜div id="optdiv">응답에 Allow 헤더가 있으면 출력됨＜/div>
＜script>
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "https://www.namusecurity.co.kr/",
  "method": "OPTIONS",
  "headers": {
    "upgrade-insecure-requests": "1",
    "accept-language": "en-US,en;q=0.9",
    "cache-control": "no-cache"
  }
}

$.ajax(settings).done(function (response) {
  document.getElementById("optdiv").innerHTML="Allow";
  console.log(response);
});
＜/script>

</code></pre>

### 대체 코드 - curl

<pre><code>

curl -I OPTIONS https://xxx.com/

</code></pre>
