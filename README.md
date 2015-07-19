# Pedestal 함수 정리

## io.pedestal.http

#### (defn edn-response [obj] ...)
obj 맵을 edn 형식으로 바꿔 ring response를 리턴해준다.

#### (defn json-print [obj] ...)
obj를 json 형식으로 `*out*`에 출력 해준다.

#### (defn json-response [obj] ...)
obj 맵을 json 형식으로 바꿔 ring response를 리턴해준다.

#### (def log-request ...)
on-request 인터셉터로 요청 Method와 URL을 log/info로 남긴다.

#### (def not-found ...)
after 인터셉터로 context의 response 값이 ring response 타입이 아닌 경우 Not Found 라는 
메시지와 404 응답코드를 가진 ring response를 context의 response에 설정한다.

#### (def html-body ...)
on-response 인터셉터로 response body가 문자열이라면 content-type에 text/html을 설정해준다.

#### (def json-body ...)
on-response 인터셉터로 response body가 컬렉션이라면 content-type에 application/json을 설정해주고
body를 json 문자열로 바꿔준다.

#### (def transit-json-body ...)
on-response 인터셉터로 response body가 컬렉션이라면 content-type에 application/transit+json을 설정해주고
body를 transit json 형태로 바꿔준다.

#### (def transit-msgpack-body ...)
on-response 인터셉터로 response body가 컬렉션이라면 content-type에 application/transit+msgpack을 설정해주고
body를 transit msgpack 형태로 바꿔준다.

#### (def transit-body ...)
transit-json-body의 alias이다.

#### (defn default-interceptors [service-map] ...)
service-map에 :interceptors 값이 없다면 기본 인터셉터를 추가한 service-map을 리턴한다.
service-map 설정 값에 따라 선택적으로 추가되는 인터셉터도 있다. 추가 되는 인터셉터들은 코드를 참고한다.

#### (defn dev-interceptors [service-map] ...)
service-map에 :interceptors 값에 개발의 편의를 위해
io.pedestal.http.cors/dev-allow-origin와 io.pedestal.http.impl.servlet-interceptor/exception-debug 인터셉터를 
추가한 service-map을 리턴한다.

#### (defn service-fn [service-map] ...)
service-map에 :service-fn 값에 인터셉터들의 io.pedestal.http.impl.servlet-interceptor/http-interceptor-service-fn 값을 추가한 service-map을 리턴한다.

#### (defn servlet [service-map] ...)
service-map에 :servlet 값에 :service-fn 값을 io.pedestal.http.servlet/servlet 함수에 적용한 결과 값을 넣는다.

#### (defn create-servlet [service-map] ...)
service-map에  default-interceptors, service-fn, servlet을 적용한 service-map을 리턴한다.

#### (defn server [service-map] ...)
service-map에 :type에 따라 jetty 서버 또는 immutant 서버 네임스페이스를 require 하고 service-map에 server 정보를 
추가해 리턴해준다.

#### (defn create-server [service-map] [service-map init-fn] ...)
init-fn (기본 값은 io.pedestal.log/init-java-util-log)를 실행하고 create-servlet, server 함수를 적용한 service-map을 리턴한다.

#### (defn start [service-map] ...)
service-map에 :start-fn 함수를 실행한다. :start-fn은 server 함수를 적용하면 생성 된다.

#### (defn stop [service-map] ...)
service-map에 :stop-fn 함수를 실행한다. :stop-fn은 server 함수를 적용하면 생성 된다.

#### (defn servlet-init [service config] ...)
service 맵에 있는 :servlet 객체(javax.servlet.Servlet)에 init 함수를 config를 인자로 실행하고 service를 리턴한다.

#### (defn servlet-destroy [service] ...)
service 맵에서 :servlet를 제거한 맵을 리턴한다.

#### (defn servlet-service [service servlet-req servlet-resp] ...)
service 맵에 있는 :servlet 객체(javax.servlet.Servlet)에 service 함수를 나머지 인자로 실행한다.

## io.pedestal.http.route
## io.pedestal.interceptor
## io.pedestal.log

