---
title: IO流的读写方法 
date: 2021-11-30
tags: 
    - 工具类
    - IO流
    - Java
---

该工具类中有两个方法：

（1） 将输入流转换成 byte[]

（2） 将输入流转换成 byte[]

<!-- more -->

## 用于演示关于流的读写方法 

- 注意：需要使用这个工具类时，把代码复制到你所写的工具类下面即可

```java
package com.javaDemo.uploaad;

import java.io.*;

/**
 * 此类用于演示关于流的读写方法
 */
public class StreamUtils {
    /**
     * 功能:将输入流转换成 byte[]
     *
     * @param is 输入流
     * @return 字节数组 array
     * @throws IOException
     */
    public static byte[] streamToByteArray(InputStream is) throws IOException {
        ByteArrayOutputStream bos = new ByteArrayOutputStream();//创建输出流对象
        byte[] b = new byte[1024];
        int len;
        while ((len = is.read(b)) != -1) {
            bos.write(b, 0, len);
        }
        byte[] array = bos.toByteArray();
        bos.close();
        return array;
    }

    /**
     * 功能:将输入流转换成 byte[]
     * @param is
     * @return
     * @throws IOException
     */
    public static String streamToString(InputStream is) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(is));
        StringBuilder sb = new StringBuilder();
        String line = "";
        while ((line = br.readLine()) != null){
            sb.append(line + "\n");
        }
        br.close();
        return sb.toString();
    }

}

```



