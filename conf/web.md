### 서블릿(tomcat, jboss; WAS) - web.xml error page

<pre><code>

＜error-page>
	＜error-code>404</error-code>
	＜location>/error/404</location>
</error-page>
＜error-page>
	＜error-code>405</error-code>
	＜location>/error/code</location>
</error-page>
＜error-page>
	＜error-code>500</error-code>
	＜location>/error/code</location>
</error-page>
＜error-page>
	＜exception-type>java.lang.Throwable</exception-type>
	＜location>/error/code</location>
</error-page>

</code></pre>

### 스프링부트 - white label error page disabled &lt;

<pre><code>

import org.springframework.boot.autoconfigure.web.ServerProperties;
import org.springframework.boot.context.embedded.ConfigurableEmbeddedServletContainer;
import org.springframework.boot.web.servlet.ErrorPage;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpStatus;
 
@Configuration
public class ErrorConfiguration extends ServerProperties
{
	@Override
	public void customize(ConfigurableEmbeddedServletContainer container)
	{
		super.customize(container);
		container.addErrorPages(new ErrorPage(HttpStatus.NOT_FOUND, "/error/404"));
		container.addErrorPages(new ErrorPage(HttpStatus.INTERNAL_SERVER_ERROR, "/error/500"));
	}
}
</code></pre>

### 대체 코드

ErrorConfiguration 클래스를 추가하고 아래 코드를 작성한다.

static에 error 폴더를 만들고 403, 404, 500을 추가한다.

<pre><code>
package com.example.demo;
import java.io.IOException;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.boot.web.servlet.error.ErrorController;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
 
@RestController
@ControllerAdvice
@Configuration
public class ErrorConfiguration  implements ErrorController {
    private static final String ERROR_PATH = "/error";

    @RequestMapping(value = "/error/{code}")
    public String handleError(@PathVariable int code) {
        String rtn = null;
        switch (code) {
            case 404:
                rtn = "Page not found";
                break;
            case 403:
        	rtn = "fobbiden";
            	break;
            case 500:
                rtn = "Internal server error";
                break;
            default:
                rtn = "error";
                break;
        }
        return rtn;
    }

    @RequestMapping(value = ERROR_PATH)
    public void handleError(HttpServletRequest request, HttpServletResponse response) throws IOException {
        response.sendRedirect("error/404");
    }

    /**
     * implement ErrorController to handle 404
     */
    public String getErrorPath() {
        return ERROR_PATH;
    }

    @ExceptionHandler(Exception.class)
    public void handleException(HttpServletRequest request, HttpServletResponse response, Exception e) throws IOException {
        response.sendRedirect("error/500");
    }
}

</code></pre>
