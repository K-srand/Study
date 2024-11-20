Todo
플레이리스트 가져올 기준 조정
webclient 리팩토링(config 파일 따로 만들어서 주입)
커뮤니티 디테일 조회 부분 수정

pageToken 하나당
playlist 50건 호출
videos 1445건 호출

1495 x 5(카테고리별) = 7,475 쿼터

--------------------------------------------------------------------------

org.springframework.web.reactive.function.client.WebClientResponseException: 200 OK from GET https://www.googleapis.com/youtube/v3/playlistItems, but response failed with cause: org.springframework.core.io.buffer.DataBufferLimitException: Exceeded limit on max bytes to buffer : 262144

대략 7000건 호출을 진행하고 있던 중 버퍼 크기 초과 에러가 발생함.
방법은 두 가지가 있다.
1. 버퍼 크기를 늘린다.
2. 카테고리도 나누어 받는다.

버퍼 사이즈 변경
```
import org.springframework.core.io.buffer.DataBufferLimitException;
import org.springframework.web.reactive.function.client.WebClient;
import org.springframework.http.client.reactive.ReactorClientHttpConnector;
import reactor.netty.http.client.HttpClient;
import reactor.netty.resources.LoopResources;

import java.time.Duration;

@Configuration
public class WebClientConfig {

    @Bean
    public WebClient webClient() {
        // 10MB로 설정 (10 * 1024 * 1024 bytes)
        int bufferSize = 10 * 1024 * 1024; // 10MB

        HttpClient httpClient = HttpClient.create()
                .responseTimeout(Duration.ofMillis(5000));

        return WebClient.builder()
                .clientConnector(new ReactorClientHttpConnector(httpClient))
                .exchangeStrategies(exchangeStrategies -> exchangeStrategies
                        .maxInMemorySize(bufferSize)) // 최대 버퍼 크기 설정
                .build();
    }
}

```