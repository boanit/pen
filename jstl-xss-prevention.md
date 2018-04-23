### jstl을 통한 xss 방어하기

jstl은 JSP Standard Tag Library의 약어로 jsp에서 자주 사용되는 태그를 커스텀하여 

라이브러리로 정의한 코드의 집합을 말합니다. 

우리는 jstl의 c:out 태그를 이용하여 출력 값에 xss 필터링을 적용할 수 있습니다.

<c:out> 태그는 jsp의 prefix 속성이 c인 core 라이브러리를 사용하는 태그로 변수를 출력할 때 사용되는 태그이며,

escapeXml 속성을 통하여 변수에 포함된 < > & ' " 문자들을 각각 &lt; &gt; &amp; &#039; &#034으로 출력합니다.

### <c:out>을 통한 xss 필터 설치

먼저  jstl 사용을 위하여 http://tomcat.apache.org/taglibs/standard/ 에서 jstl 1.1 버전을 설치합니다.

설치 후 lib 디렉토리에서 jstl.jar, standard.jar 파일을 WEB-INF/lib 디렉토리로 복사합니다.

 필터를 적용할 jsp파일에서 jstl core 사용을 위한 선언을 합니다.

<pre><code><%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
</code></pre>

### <c:out> 태그 적용하기

<pre><code>
<p> input data : <%=data %>
<p> <c:out value="${param.data }"[escapeXml="{true|false}"]></c:out></p>
</code></pre>

* escapeXml은 생략될 경우 default로 true가 설정되며 < > & ' " 문자들을 각각 &lt; &gt; &amp; &#039; &#034; 로 출력됩니다.