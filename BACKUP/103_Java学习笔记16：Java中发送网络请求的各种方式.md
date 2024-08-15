# [Java学习笔记16：Java中发送网络请求的各种方式](https://github.com/QiYongchuan/MyGitBlog/issues/103)

 **1.使用 Java 原生的 HttpURLConnection** 
 ```java
private JSONObject sendHttpRequest(String requestURI, JSONObject jsonBody) throws IOException, BusinessException, JSONException {
    String access_token = nc.bs.einvoice.util.BillEffectUtils.ensureToken();
    HttpURLConnection debtorsRequest = (HttpURLConnection) new URL(requestURI).openConnection();
    debtorsRequest.setRequestMethod("POST");
    debtorsRequest.setRequestProperty("Authorization", "Bearer " + access_token);
    debtorsRequest.setRequestProperty("Content-Type", "application/json");
    debtorsRequest.setRequestProperty("Accept", "*/*");
    debtorsRequest.setDoOutput(true);
    
    try (OutputStream os = debtorsRequest.getOutputStream()) {
        byte[] input = jsonBody.toString().getBytes("utf-8");
        os.write(input, 0, input.length);
    }

    int responseCode = debtorsRequest.getResponseCode();
    if (responseCode == HttpURLConnection.HTTP_OK || responseCode == HttpURLConnection.HTTP_CREATED) {
        BufferedReader reader = new BufferedReader(new InputStreamReader(debtorsRequest.getInputStream()));
        StringBuilder response = new StringBuilder();
        String line;
        while ((line = reader.readLine()) != null) {
            response.append(line);
        }
        return new JSONObject(response.toString());
    } else {
        handleError(debtorsRequest);
        return null; 
    }
}

private void handleError(HttpURLConnection debtorsRequest) throws IOException, JSONException, BusinessException {
    BufferedReader errorResponseReader = new BufferedReader(new InputStreamReader(debtorsRequest.getErrorStream()));
    StringBuilder errorResponseText = new StringBuilder();
    String errorLine;
    while ((errorLine = errorResponseReader.readLine()) != null) {
        errorResponseText.append(errorLine);
    }
    JSONObject errorResponse = new JSONObject(errorResponseText.toString());
    String errorMessage = errorResponse.optString("message", "Unknown error");
    JSONObject errors = errorResponse.optJSONObject("errors");
    throw new BusinessException("Error from API: " + errorMessage + "  \\nDetails: " + errors);
}

```


---

**2. 使用 Apache HttpClient**
```java
public static JSONObject doPost(String url, Map<String, Object> payload, Map<String, String> headers) throws BusinessException {  
    HttpPost httpPost = new HttpPost(url);    
    JSONObject jsonObject = new JSONObject(payload); // 直接将Map转换为JSONObject  
    StringEntity entity = new StringEntity(jsonObject.toString(), "UTF-8");  
    httpPost.setEntity(entity);  
    httpPost.setHeader("Content-Type", "application/json");  
    if (headers != null) {  
        headers.forEach(httpPost::addHeader);  
    }  
    
    try (CloseableHttpResponse response = httpClient.execute(httpPost)) {  
        JSONObject jsonObjectRes = handleResponse(response);  
        return jsonObjectRes;  
    } catch (IOException | BusinessException | JSONException e) {  
        throw new BusinessException("执行POST请求失败", e);  
    }  
}

private static JSONObject handleResponse(CloseableHttpResponse response) throws BusinessException, JSONException {  
    int statusCode;
    String jsonResponse;
    try {
        statusCode = response.getStatusLine().getStatusCode();
        jsonResponse = EntityUtils.toString(response.getEntity());
    } catch (IOException e) {
        throw new BusinessException("网络请求失败: " + e.getMessage(), e);
    }

    if (statusCode >= 200 && statusCode <= 300) {
        if (statusCode == HttpStatus.SC_NO_CONTENT) {
            return new JSONObject(); // 或者返回null，具体取决于业务逻辑
        }
        
        if (jsonResponse.trim().startsWith("[")) {
            JSONArray jsonArray = new JSONArray(jsonResponse);
            if (jsonArray.length() == 0) {
                JSONObject fixedJson = new JSONObject();
                fixedJson.put("message", "old_invoice");
                return fixedJson;
            }
            JSONObject lastElement = jsonArray.getJSONObject(jsonArray.length() - 1);
            return lastElement;
        } else {
            return new JSONObject(jsonResponse);
        }
    } else if (statusCode == 400 || statusCode == 401 || statusCode == 404) {
        JSONObject errorResponse = new JSONObject(jsonResponse);
        String errorMessage = errorResponse.getString("message");
        String status = errorResponse.getString("status");
        JSONObject errors = errorResponse.getJSONObject("errors");
        throw new BusinessException("Status: " + status + "\nError from API: " + errorMessage + "  \nDetails: " + errors);
    } else {
        throw new BusinessException("HTTP请求失败: 状态码 " + statusCode);
    }
}

```

---

![image](https://github.com/user-attachments/assets/56306e4e-d716-458f-a610-7e3603f5016f)
