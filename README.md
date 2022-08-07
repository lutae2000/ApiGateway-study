# ApiGateway-study
study for micro service - API gateway 

```
  GatewayFilter filter = new OrderedGatewayFilter((exchange, chain) -> {
      ServerHttpRequest request = exchange.getRequest();
      ServerHttpResponse response = exchange.getResponse();

      log.info("Logging filter baseMessage: {}", config.getBaseMessage());

      if(config.isPreLogger()){
          log.info("Logging filter start: request id -> {}", request.getId());
      }
      return chain.filter(exchange).then(Mono.fromRunnable(() -> {
          if(config.isPostLogger()){
              log.info("Logging Post end: response code -> {}", response.getStatusCode());
          }
      }));
  }, Ordered.HIGHEST_PRECEDENCE);
  ```
  
Ordered.HIGHEST_PRECEDENCE 조건에 따라 실행되는 필터의 우선순위가 달라짐

LOWEST_PRECEDENCE 일 경우 아래의 순서대로 실행 됨
1. Global filter
2. Custom filter
3. Logging filter
