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
