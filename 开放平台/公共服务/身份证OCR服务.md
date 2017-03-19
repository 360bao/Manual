# 身份证OCR服务

- 通过POST将两张图片（身份证正反面）上传到https://bit-s.cc/platform/foundation/ocr/idcard，Content-Type需要为multipart/form-data
- 如果使用jsonp，则在url中带入参数callback
- 下面是示例(cURL)：
```cURL
curl -X POST -H "Cache-Control: no-cache" -H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" -F "idcard=@001fd04ce7380e39fb351a.jpg" -F "idcard=@1-121015111H34E.jpg" "https://bit-s.cc/platform/foundation/ocr/idcard?callback=f123"
```
