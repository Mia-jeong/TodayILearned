# URL encoding이 필요한 이유



### 1. URL Encoding 이 필요한 이유



- URL encoding은 URL 스트링에 있는 정보를 모든 브라우저에 올바르게 전송하기 위해 필요한 작업이다.
- 인터넷의 URL은 ASCII 문자열을 이용해서만 전송이 가능 하다. 해당 문자열 외에 다른 문자열을 전송한 경우 브라우저 특성에 따라 잘리거나 변형이 될 수 있다. 그렇기 때문에 이러한 특수문자는 encoding이 되는 것이 좋다 특히 ASCII에 포함되지 않은 문자들은 encoding이 필요하다.
- URL encoding은 안전하지 않은 ASCII 문자를 `%` 다음에 두 개의 16진수 로 대체한다.
- URL은 공백을 포함할 수 없다. 공백은 URL encoding을 통해 `+` 혹은 `%20` 으로 바 꾼다.
- ASCII Encoding Reference 는 다음 링크에서 확인 가능하다 [HTML URL Encode](https://www.w3schools.com/tags/ref_urlencode.asp)

- [URL Decoder/Encoder](https://meyerweb.com/eric/tools/dencoder/)

### 2. Character Encoding Chart

| Classification           | Included characters                                          | Encoding required |
| ------------------------ | ------------------------------------------------------------ | ----------------- |
| Safe characters          | Alphanumerics `[0-9a-zA-Z]`, special characters `$-_.+!*'(),`, and reserved characters used for their reserved purposes (e.g., question mark used to denote a query string) | **NO**            |
| ASCII Control characters | Includes the ISO-8859-1 (ISO-Latin) character ranges 00-1F hex (0-31 decimal) and 7F (127 decimal.) | **YES**           |
| Non-ASCII characters     | Includes the entire “top half” of the ISO-Latin set 80-FF hex (128-255 decimal.) | **YES**           |
| Reserved characters      | `; / ? : @ = &` (does not include blank space)               | **YES**1          |
| Unsafe characters        | Includes the blank/empty space and " < > # % { } \| \ ^  ~ [ ]  ` | **YES**           |

> 1 *Reserved characters only need encoded when not used for their defined, reserved purposes.*

출처: [(Please) Stop Using Unsafe Characters in URLs](https://perishablepress.com/stop-using-unsafe-characters-in-urls/)

