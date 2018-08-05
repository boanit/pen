### 자바 - 기본적인 필터링 함수

조합 가능한 특수 문자와 확장자를 제거한다.

<pre><code>

public static String xpathi(String filepath) {
filepath = filepath.replaceAll("[","");
filepath = filepath.replaceAll ("]","");
filepath = filepath.replaceAll ("/","");
filepath = filepath.replaceAll ("'","");
return filepath;
}
public static String cmdi(String filepath) {
filepath = filepath.replaceAll("|","");
filepath = filepath.replaceAll (";","");
filepath = filepath.replaceAll (">","");
filepath = filepath.replaceAll (" ","");
return filepath;
}
public static String download(String filepath) {
filepath = filepath.replaceAll("/","");
filepath = filepath.replaceAll ("\\\\","");
filepath = filepath.replaceAll ("\\.","");
filepath = filepath.replaceAll ("&","");
return filepath;
}
public static String fileext(String value) {
final String[] BAD_EXTENSION = { "jsp", "php", "asp", "html", "perl" };

try {
int len = BAD_EXTENSION.length;
for (int i = 0; i < len; i++) {
if (value.equalsIgnoreCase(BAD_EXTENSION[i])) {
System.out.println("BAD EXTENSION FILE UPLOAD");
throw new IOException("BAD EXTENSION FILE UPLOAD");
}
}
} catch (IOException e) {
e.printStackTrace();
}
return value;
}

</code></pre>

### 정규식 - regex.Pattern 라이브러리 사용 코드가 가능하다.

<pre><code>

import java.util.regex.Pattern;
public class HelloWorld{
public static String cleanSQLI(String value) {
final Pattern SpecialChars = Pattern.compile("['\"\\-#()@;=*/+]");
value = SpecialChars.matcher(value).replaceAll("");
return value;
}
public static String cleanXSS(String value) {
//You'll need to remove the spaces from the html entities below
value = value.replaceAll("<", "& lt;").replaceAll(">", "& gt;");
value = value.replaceAll("\\(", "& #40;").replaceAll("\\)", "& #41;");
value = value.replaceAll("'", "& #39;");
value = value.replaceAll("eval\\((.*)\\)", "");
value = value.replaceAll("[\\\"\\\'][\\s]*javascript:(.*)[\\\"\\\']", "\"\"");
value = value.replaceAll("script", "");
return cleanSQLI(value);
}
public static void main(String []args){
System.out.println(cleanSQLI("#'unn--"));
}
}

</code></pre>

### 더블 인코딩

https://www.owasp.org/index.php/Double_Encoding

<pre><code>

String t1 = "%253Ctest<".replaceAll("%253C", "");

</code></pre>
