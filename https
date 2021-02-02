웹사이트 로그인 시 보안을 위해 HTTPS로 접근하여 로그인을 처리한다. 이후 웹사이트 이용 중 HTTP로 프로토콜 전환이 발생할 때 웹 브라우저는 세션을 읽어오지 못하는 증상이 발생한다.

좀더 세부적으로 두가지 상황이 존재한다.

1. Index 페이지에 HTTP로 접속 -> Login 페이지로 이동하여 HTTPS로 접속하여 로그인 처리 후 세션 쿠키 발행 -> 이후 다른 페이지 이용시 HTTP로 이용 (HTTP -> HTTPS -> HTTP)
2. Login 페이지에 HTTPS로 바로 접속하여 로그인 처리 후 세션 쿠키 발행 -> 이후 다른 페이지 이용시 HTTP로 이용 (HTTPS -> HTTP)

위 두 경우에서 1번의 경우는 세션이 잘 유지되고, 2번의 경우는 세션이 유지되지 못한다.

로그인을 HTTPS에서 처리하였느냐와 관계없이 위 두 경우의 차이는 웹사이트에 **"최초 접속시"** HTTP로 접근하였느냐, HTTPS로 접근하였느냐의 차이이다. 웹사이트 최초 접속 시 HTTPS로 접근하면 HTTP와는 달리 `Secure` Flag가 적용된 Secure Cookie를 발행한다. 이 Secure Cookie는 HTTP 하에서는 인식하지 못한다. 반대로 웹사이트 최초 접속 시 HTTP로 접근하여 `Secure` Flag가 없는 Non-secure Cookie를 발행하게 되면 이후 HTTPS로 접근한다고 하여도 Secure Cookie를 추가적으로 발급하지 않는다. 다만 HTTPS에서는 Non-secure Cookie 역시 정상적으로 인식한다. 정리하면 아래와 같다.

1. 최초 HTTP 접속 (Non-secure Cookie발행) -> HTTPS 접근 (Non-Secure Cookie 정상 인식) -> HTTP 접근 (Non-Secure Cookie 정상 인식) -> 웹사이트 정상 사용
2. 최초 HTTPS 접속 (Secure Cookie 발행) -> HTTP 접근 (Secure Cookie 인식 불가) -> 웹사이트 세션 이용 불가



## 일반적인 해결방법

엄밀히 말하면 위의 상황이 발생하는 것 자체를 피하는 것이 바람직 한 해결 방법이다. 웹사이트에 로그인 기능이 존재한다면, 개인정보 해킹의 위험을 방지하기 위해 HTTPS 프로토콜을 이용하는 것이 맞고, 세션 로그인을 한 뒤에 HTTP로 전환하여 세션을 유지시키려고 한다면 여전히 해킹의 위험이 남아있게 되는 것이다. 또한 최초 접속 역시 HTTP로 하게 되면 Secure Cookie를 발급하지 못하게 되어 역시 보안 위험에 처하게 된다.

결국 전체 웹사이트를 HTTPS로 통합하여 사용하도록 수정하는 것이 바람직 하다. 이를 강제하기 위해 Tomcat의 conf/web.xml에 Secure 옵션을 설정하는것을 권고한다. 이 옵션을 설정하면 웹브라우저에서 HTTPS로 접속한 경우에만 Cookie를 발행한다. 당연히 Secure Cookie가 발행된다.

```null
<session-config>
  <cookie-config>
    <secure>true</secure>
  </cookie-config>
</session-config>
```





## 설정으로 해결

그럼에도 불구하고 HTTP 하에서도 세션을 유지하길 바란다면 Secure Cookie가 발급될 때 Secure Flag를 강제로 누락시키는 방법이 있다. Tomcat 앞에 Apache Web Server를 두어 연동한뒤, conf/httpd.conf에 mod_header를 이용하여 Secure Flag를 삭제한다.

```null
LoadModule headers_module modules/mod_headers.so
<IfModule mod_headers.c>
  Header edit* Set-Cookie "(JSESSIONID=.*)(; Secure)" "$1"
</IfModule>
```





## 정리

HTTP <-> HTTPS 전환 시에 세션이 유지되지 않는 현상에 대하여 정리해보았다. 위에서도 언급했듯이, 이 문제를 설정으로 해결하는 것은 오히려 Secure Flag를 누락시킴으로서 보안상 안전하지 않다. 이 문제의 해결방법은 전체를 HTTPS로 통일하는 것임을 명심하도록 하자.
