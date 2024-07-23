# [OpenApiUtil ：封装调用接口的方法](https://github.com/QiYongchuan/MyGitBlog/issues/99)

```
package nc.bs.einvoice.util;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;

import nc.vo.pub.BusinessException;

import org.apache.commons.httpclient.HttpStatus;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.util.Map;


public class OpenApiUtil {

    private static CloseableHttpClient httpClient = HttpClients.createDefault();

    /**
     * 执行GET请求并返回指定类型的响应。
     * @throws BusinessException 
     */
    public static <T> T doGet(String url, Map<String, String> headers, Class<T> responseType) throws BusinessException {  
        HttpGet httpGet = new HttpGet(url);  
        if (headers != null) {  
            headers.forEach(httpGet::addHeader);  
        }  
      
        try (CloseableHttpResponse response = httpClient.execute(httpGet)) {  
            JSONObject jsonObject = handleResponse(response);  
            return JSON.parseObject(jsonObject.toJSONString(), responseType);  
        } catch (IOException | BusinessException e) {  
            throw new BusinessException("执行GET请求失败", e);  
        }  
    } 

    /**
     * 执行POST请求，发送JSON数据，并返回指定类型的响应。
     */
    public static <T> T doPost(String url, Object payload, Map<String, String> headers, Class<T> responseType) {  
        HttpPost httpPost = new HttpPost(url);  
        StringEntity entity = new StringEntity(JSON.toJSONString(payload), "UTF-8");  
        httpPost.setEntity(entity);  
        httpPost.setHeader("Content-Type", "application/json");  
        if (headers != null) {  
            headers.forEach(httpPost::addHeader);  
        }  
      
        try (CloseableHttpResponse response = httpClient.execute(httpPost)) {  
            JSONObject jsonObject = handleResponse(response);  
            return JSON.parseObject(jsonObject.toJSONString(), responseType);  
        } catch (IOException | BusinessException e) {  
            throw new RuntimeException("执行POST请求失败", e);  
        }  
    }

    /**
     * 处理HTTP响应的通用逻辑。
     * @throws BusinessException 
     */
    private static JSONObject handleResponse(CloseableHttpResponse response) throws  BusinessException {  
	        int statusCode;
	        String jsonResponse;
	    	try {
	    		 statusCode = response.getStatusLine().getStatusCode();
	    	     jsonResponse = EntityUtils.toString(response.getEntity());
	    		} catch (IOException e) {
	    	        // 捕获 IOException 并重新抛出为 BusinessException
	    	        throw new BusinessException("网络请求失败: " + e.getMessage(), e);
	    	    }
    	
    	    if (statusCode >= 200 && statusCode <= 300) {
    	        if (statusCode == HttpStatus.SC_NO_CONTENT) {
    	            return new JSONObject(); // 或者返回null，具体取决于业务逻辑
    	        }
    	        return JSON.parseObject(jsonResponse);
    	    } else if (statusCode == 400) {
    	        JSONObject errorResponse = JSON.parseObject(jsonResponse.toString());
    	        String errorMessage = errorResponse.getString("message");
    	        if (errorMessage == null) {
    	            errorMessage = "Unknown error";
    	        }
    	        String status = errorResponse.getString("status");
    	        if (status == null) {
    	            status = "Unknown status";
    	        }
    	        JSONObject errors = errorResponse.getJSONObject("errors");
    	        throw new BusinessException("Status: " + status + "\nError from API: " + errorMessage + "  \nDetails: " + errors);
    	    } else {
    	        // 对其他错误状态码的处理可以类似地扩展
    	        throw new BusinessException("HTTP请求失败: 状态码 " + statusCode);
    	    }
    	}
    }
```

---

非泛型，仅支持返回json object类型的方法
```
package nc.bs.einvoice.util;

//import com.alibaba.fastjson.JSON;
//import com.alibaba.fastjson.JSONObject;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;
import nc.vo.pub.BusinessException;

import org.apache.commons.httpclient.HttpStatus;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.util.Map;


public class OpenApiUtil {

    private static CloseableHttpClient httpClient = HttpClients.createDefault();

    /**
     * 执行GET请求并返回指定类型的响应。
     * @throws BusinessException 
     */
    public static JSONObject doGet(String url, Map<String, String> headers) throws BusinessException {  
        HttpGet httpGet = new HttpGet(url);  
        if (headers != null) {  
            headers.forEach(httpGet::addHeader);  
        }  
      
        try (CloseableHttpResponse response = httpClient.execute(httpGet)) {  
            JSONObject jsonObject = handleResponse(response);  
            return   jsonObject;
        } catch (IOException | BusinessException | JSONException e) {  
            throw new BusinessException("执行GET请求失败", e);  
        }  
    } 

    /**
     * 执行POST请求，发送JSON数据，并返回指定类型的响应。
     * @throws BusinessException 
     */
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

    /**
     * 处理HTTP响应的通用逻辑。
     * @throws BusinessException 
     * @throws JSONException 
     */
    private static JSONObject handleResponse(CloseableHttpResponse response) throws  BusinessException, JSONException {  
	        int statusCode;
	        String jsonResponse;
	    	try {
	    		 statusCode = response.getStatusLine().getStatusCode();
	    	     jsonResponse = EntityUtils.toString(response.getEntity());
	    		} catch (IOException e) {
	    	        // 捕获 IOException 并重新抛出为 BusinessException
	    	        throw new BusinessException("网络请求失败: " + e.getMessage(), e);
	    	    }
    	
    	    if (statusCode >= 200 && statusCode <= 300) {
    	        if (statusCode == HttpStatus.SC_NO_CONTENT) {
    	            return new JSONObject(); // 或者返回null，具体取决于业务逻辑
    	        }
    	        return new JSONObject(jsonResponse);
    	    } else if (statusCode == 400) {
    	        JSONObject errorResponse = new JSONObject(jsonResponse.toString());
    	        String errorMessage = errorResponse.getString("message");
    	        if (errorMessage == null) {
    	            errorMessage = "Unknown error";
    	        }
    	        String status = errorResponse.getString("status");
    	        if (status == null) {
    	            status = "Unknown status";
    	        }
    	        JSONObject errors = errorResponse.getJSONObject("errors");
    	        throw new BusinessException("Status: " + status + "\nError from API: " + errorMessage + "  \nDetails: " + errors);
    	    } else {
    	        // 对其他错误状态码的处理可以类似地扩展
    	        throw new BusinessException("HTTP请求失败: 状态码 " + statusCode);
    	    }
    	}
    }
```