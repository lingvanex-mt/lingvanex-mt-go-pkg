# Lingvanex API

[![Go Reference](https://pkg.go.dev/badge/github.com/lingvanex-mt/lingvanex-mt-go-pkg.svg)](https://pkg.go.dev/github.com/lingvanex-mt/lingvanex-go-pkg)

Discover the Power of Lingvanex Translator Service

Unlock the potential of your applications with Lingvanex Translator, a cutting-edge cloud-based neural machine translation service. Compatible with any operating system, Lingvanex Translator enables the creation of intelligent, multi-lingual solutions for all supported languages.

With Lingvanex, you can effortlessly translate both text and HTML pages, enhancing your global reach and communication capabilities. Explore the capabilities of the [Lingvanex Cloud API](https://lingvanex.com/translationapi/) and learn more about our [Secure On-Premise Machine Translation](https://lingvanex.com/).

## How to get the authentication key

Before using the API you need to create the [account](https://lingvanex.com/account/) and then generate the API key at the bottom of the page. You must use this authorization key to authorize requests.

## Installation

You can install the library:

```bash
go install github.com/lingvanex-mt/lingvanex-go-pkg
```

## Getting the list of languages

To retrieve the list of languages, perform a GET request with the authentication key as follows:

```go
package main

import (
	"fmt"
	"net/http"
	"io"
)

func main() {
	url := "https://api-b2b.backenster.com/b1/api/v3/getLanguages?platform=api&code=en_GB"

	req, _ := http.NewRequest("GET", url, nil)

	req.Header.Add("accept", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := io.ReadAll(res.Body)

	fmt.Println(string(body))
}
```

Options:

- `url`: [https://api-b2b.backenster.com/b1/api/v3/getLanguages](https://api-b2b.backenster.com/b1/api/v3/getLanguages)
- `platform`: api
- `Authorization`: The key must be obtained in advance
- `code`: the language code in the format “language code_code of the country”, which is used to display the names of the languages. The language code is represented only in lowercase letters, the country code only in uppercase letters (example en_GB, es_ES, ru_RU etc). If this option is not present, then English is used by default.

## Translate

This POST method translates text and HTML single string or arrays with the authentication key. Also it performs transliteration, language auto detection.

```go
package main

import (
	"fmt"
	"strings"
	"net/http"
	"io"
)

func main() {
	url := "https://api-b2b.backenster.com/b1/api/v3/translate"

	payload := strings.NewReader("{\"platform\":\"api\"}")

	req, _ := http.NewRequest("POST", url, payload)

	req.Header.Add("accept", "application/json")
	req.Header.Add("content-type", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := io.ReadAll(res.Body)

	fmt.Println(string(body))
}
```

Options:

- `url`: [https://api-b2b.backenster.com/b1/api/v3/translate](https://api-b2b.backenster.com/b1/api/v3/translate)
- `platform`: api
- `Authorization`: The key must be obtained in advance
- `from`: the language code in the format “language code_code of the country” from which the text is translated. The language code is represented only in lowercase letters, the country code only in uppercase letters (example en_GB, es_ES, ru_RU and etc.). If this parameter is not present, the auto-detect language mode is enabled.
- `to`: language code in the format “language code_code of the country” to which the text is translated (required)
- `data`: data for translation.
- `translateMode`: Describe the input text format. Possible value is "html" for translating and preserving html structure. If value is not specified or is other than "html" than plain text is translating.
- `enableTransliteration`: If true response includes sourceTransliteration and targetTransliteration fields.

## Issues

If you are having problems using the library, please [contact](https://lingvanex.com/contact-us/) us.
