---
title: CORS(Cross-Origin Resource Sharing )
date: "2022-06-13T22:12:03.284Z"
---
- **브라우저의 동일 근원 정책에 의해 생겨난 타 도메인 간에 자원을 공유할 수 있게 해주는 것**
    - **동일근원 정책이란 ?**
        - 다른 도메인으로부터 리소스가 요청될 경우 해당 리소스는 `cross-origin HTTP` 요청에 의해 요청되나 대부분의 브라우저들은 보안상의 이유로 스크립트에서 `cross-origin HTTP` 요청을 제한한다. 이것을 `Same-Origin-Policy`(동일 근원 정책)이라고 한다. 요청을 보내기 위해서는 요청을 보내고자 하는 대상과 프로토콜 및 포트가 같아야 함을 의미한다.
    - **해결방안**
        - 과거에는 flash를 proxy로 두고 타 도메인간 통신을 했으나 모바일 운영체제(IOS에서는 flash자체를 지원하지 않음)의 등장으로 제한
        - JSONP(json-padding)
            - `JSONP`란 jQuery v1.2이상 부터 지원되며, ajax호출 시 타 도메인 간에 호출이 가능 하게 해준다. 타 도메인간 자원 공유할 수 있는 몇가지 태그가 존재하는데 예를 들면 `img`, `iframe`, `anchor`, `script`, `link` 등이 존재한다.
        - Preflight Request(request.setHeader())
            - 실제 요청을 보내도 안전한지 판단하기 위해 `preflight` 요청을 먼저 보내는 방법, 실제 요청 전에 인증 헤더를 전송하여 서버의 허용 여부를 미리 체크하는 테스트 요청 이 요청으로 인해 트래픽이 증가할 수 있는데 서버의 헤더 설정으로 캐쉬가 가능 HTTP의 `OPTIONS` 메서드를 사용하며 `Access-Control-Request` 형태의 헤더로 전송함으로 써 브라우저가 해당 도메인에서 CORS를 허용하는지 알 수 있다.
            - | `HTTP Header` | `Description` |
              | --- | --- |
              | Access-Control-Allow-Origin | 접근 가능한 url 설정 |
              | Access-Control-Allow-Credentials | 접근 가능한 쿠키 설정 |
              | Access-Control-Allow-Headers | 접근 가능한 헤더 설정 |
              | Access-Control-Allow-Methods | 접근 가능한 http method 설정 |

            - REST API를 통한 처리
              - 클라이언트에서 바로 처리하지 않고 서버 단에서 `REST API`를 활용해 서버간에 응답 데이터를 받아와 클라이언트에 데이터를 전달해 주는 방식이다.