
```shell
http://121.37.174.241/#/digitalDiaphragm?ticket=NzK%2aL3#!Bumu25pA

# 旧地址
curl -X GET "http://121.37.177.42/token/generate?appid=8gr2wFXWTvsNcPZQ&secret=eJIF2pIsQlNxrVTp4jOFZLjwh6ZX4KDU"

curl -X POST "http://121.37.177.42/openapi/getProductQualityForecast" \
  -H "Authorization: agoLELzRsSBRv6fmlpqiOClkzBNcxN0B" \
  -H "Content-Type: application/json" \
  -d '{"productDate": "2023-04-18", "productId": "2023-04-18_1350", "productSectionId": "Y01"}'

# 新地址
curl -X GET "http://121.37.176.250/token/generate?appid=8gr2wFXWTvsNcPZQ&secret=eJIF2pIsQlNxrVTp4jOFZLjwh6ZX4KDU"

curl -X POST "http://121.37.176.250/openapi/getProductQualityForecast" \
  -H "Authorization: agoLELzRsSBRv6fmlpqiOClkzBNcxN0B" \
  -H "Content-Type: application/json" \
  -d '{"productDate": "2023-04-18", "productId": "2023-04-18_1350", "productSectionId": "Y01"}'
```
