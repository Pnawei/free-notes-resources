---
title: 播放音乐的线程类 
date: 2021-12-05
tags: 
    - 工具类
    - IO流
    - Java
---

该工具类使用说明：

主函数中在面板组件构造函数的 最后 实现 播放音乐的线程  语句: new AePlayWave("文件路径").start(); 

<!-- more -->

## 用于实现自动播放音乐的线程类 

- 注意：需要使用这个工具类时，把代码复制到你所写的工具类下面即可

```java
package com.tankgame.tankgame04;

import javax.sound.sampled.*;
import java.io.File;
import java.io.IOException;

/**
 * @author Ping
 * @version 1.0
 * 使用说明：主函数中在面板组件构造函数的 最后 实现 播放音乐的线程  语句: new AePlayWave("文件路径").start();
 */
public class AePlayWave extends Thread {
    private String fileName;

    public AePlayWave(String wavefile) {
        fileName = wavefile;
    }

    @Override
    public void run() {
        File soundFile = new File(fileName);

        AudioInputStream audioInputStream = null;
        try {
            audioInputStream = AudioSystem.getAudioInputStream(soundFile);
        } catch (UnsupportedAudioFileException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
            return;
        }
        AudioFormat format = audioInputStream.getFormat();
        SourceDataLine auLine = null;
        DataLine.Info info = new DataLine.Info(SourceDataLine.class, format);

        try {
            auLine = (SourceDataLine) AudioSystem.getLine(info);
            auLine.open(format);
        } catch (LineUnavailableException e) {
            e.printStackTrace();
            return;
        }

        auLine.start();
        int nBytesRead = 0;
        //这是缓冲区
        byte[] abData = new byte[512];

        while (nBytesRead != -1) {
            try {
                nBytesRead = audioInputStream.read(abData, 0, abData.length);
            } catch (IOException e) {
                e.printStackTrace();
                return;
            } finally {
                auLine.drain();
                auLine.close();
            }
        }
    }

}

```
