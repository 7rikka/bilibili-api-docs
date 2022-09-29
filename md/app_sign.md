# App端sign参数说明

APP端请求需要携带sign参数用于校验参数合法性，需要使用对应的`appkey`和`appsecret`进行计算

不同的APP使用不同的appkey

# App端sign计算方式

1. 对url参数进行升序排序
2. 将参数**按顺序**处理为字符串，格式为`key=value`，并使用`&`拼接，最终格式：`key1=value1&key2=value2&key3=value3`
3. 得到处理后的字符串，将`appsecret`拼接到末尾，不需要添加额外的连接字符
4. 对拼接后的字符串进行md5计算，得到结果长度为32的小写字符串，为sign值
5. 将sign放到请求中

# 生成示例

## Java实现

```java
import cn.hutool.crypto.SecureUtil;

import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;
import java.util.StringJoiner;

public class AppUtil {
    public static String getSign(Map<String, String> map, String appSecret) {
        StringJoiner sj = new StringJoiner("&");
        Object[] keyArray = map.keySet().toArray();
        Arrays.sort(keyArray);
        for (Object key : keyArray) {
            sj.add(key + "=" + map.get((String) key));
        }
        return SecureUtil.md5(sj + appSecret);
    }

    public static void main(String[] args) {
        String appKey = "8d23902c1688a798";
        String appSecret = "710f0212e62bd499b8d3ac6e1db9302a";
        Map<String, String> map = new HashMap<>();
        map.put("appkey", appKey);
        map.put("local_id", "0");
        map.put("mobi_app", "android_bilithings");
        map.put("ts", "1664435004");
        String sign = getSign(map, appSecret);
        System.out.println(sign); // 573c48ef19383297aab5891d86c19ddb
    }
}

```