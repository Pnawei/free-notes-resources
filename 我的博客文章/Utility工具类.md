---
title: 处理用户输入情况的工具类
date: 2021-11-18
tags: 
    - 工具类
    - Utility
    - Java
---

最近学习java，做项目体会思路，听老韩讲的一些知识，眼界一下子开阔了许多。其中说到，我们在实际开发中，公司都会提供相应的工具类和开发库，来提高开发效率。

对于这些工具类或开发库，我们可以直接使用，这样就省了我们一大半的时间在写处理这种情况的代码，我们可以直接使用别人已经写好的处理这种情况的代码（工具类）。例：我现在做的一个项目，就使用到了一个工具类（功能时：处理各种情况的用户输入），下面时代码分享，需要用时可取，不谢。

<!-- more -->

## 处理用户输入情况的工具类

### 工具类的作用

- 处理各种情况的用户输入，并且能够按照程序员的需求，得到用户的控制台输入。
- 注意：需要使用这个工具类时，把代码复制到你所写的工具类下面即可

```java
package com.houserent.utils; //在这个包下
/**
	工具类的作用:
	处理各种情况的用户输入，并且能够按照程序员的需求，得到用户的控制台输入。
*/
import java.util.*;

public class Utility {
	//静态属性。。。
    private static final Scanner scanner = new Scanner(System.in);

    
    /**
     * 功能：读取键盘输入的一个菜单选项，值：1——5的范围
     * @return 1——5
     */
	public static char readMenuSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1, false);//包含一个字符的字符串
            c = str.charAt(0);//将字符串转换成字符char类型
            if (c != '1' && c != '2' && 
                c != '3' && c != '4' && c != '5') {
                System.out.print("选择错误，请重新输入：");
            } else break;
        }
        return c;
    }

	/**
	 * 功能：读取键盘输入的一个字符
	 * @return 一个字符
	 */
    public static char readChar() {
        String str = readKeyBoard(1, false);//就是一个字符
        return str.charAt(0);
    }
    /**
     * 功能：读取键盘输入的一个字符，如果直接按回车，则返回指定的默认值；否则返回输入的那个字符
     * @param defaultValue 指定的默认值
     * @return 默认值或输入的字符
     */
    
    public static char readChar(char defaultValue) {
        String str = readKeyBoard(1, true);//要么是空字符串，要么是一个字符
        return (str.length() == 0) ? defaultValue : str.charAt(0);
    }
	
    /**
     * 功能：读取键盘输入的整型，长度小于2位
     * @return 整数
     */
    public static int readInt() {
        int n;
        for (; ; ) {
            String str = readKeyBoard(10, false);//一个整数，长度<=10位
            try {
                n = Integer.parseInt(str);//将字符串转换成整数
                break;
            } catch (NumberFormatException e) {
                System.out.print("数字输入错误，请重新输入：");
            }
        }
        return n;
    }
    /**
     * 功能：读取键盘输入的 整数或默认值，如果直接回车，则返回默认值，否则返回输入的整数
     * @param defaultValue 指定的默认值
     * @return 整数或默认值
     */
    public static int readInt(int defaultValue) {
        int n;
        for (; ; ) {
            String str = readKeyBoard(10, true);
            if (str.equals("")) {
                return defaultValue;
            }
			
			//异常处理...
            try {
                n = Integer.parseInt(str);
                break;
            } catch (NumberFormatException e) {
                System.out.print("数字输入错误，请重新输入：");
            }
        }
        return n;
    }

    /**
     * 功能：读取键盘输入的指定长度的字符串
     * @param limit 限制的长度
     * @return 指定长度的字符串
     */

    public static String readString(int limit) {
        return readKeyBoard(limit, false);
    }

    /**
     * 功能：读取键盘输入的指定长度的字符串或默认值，如果直接回车，返回默认值，否则返回字符串
     * @param limit 限制的长度
     * @param defaultValue 指定的默认值
     * @return 指定长度的字符串
     */
	
    public static String readString(int limit, String defaultValue) {
        String str = readKeyBoard(limit, true);
        return str.equals("")? defaultValue : str;
    }


	/**
	 * 功能：读取键盘输入的确认选项，Y或N
	 * 将小的功能，封装到一个方法中.
	 * @return Y或N
	 */
    public static char readConfirmSelection() {
        System.out.println("请输入你的选择(Y/N): 请小心选择");
        char c;
        for (; ; ) {//无限循环
        	//在这里，将接受到字符，转成了大写字母
        	//y => Y n=>N
            String str = readKeyBoard(1, false).toUpperCase();
            c = str.charAt(0);
            if (c == 'Y' || c == 'N') {
                break;
            } else {
                System.out.print("选择错误，请重新输入：");
            }
        }
        return c;
    }

    /**
     * 功能： 读取一个字符串
     * @param limit 读取的长度
     * @param blankReturn 如果为true ,表示 可以读空字符串。 
     * 					  如果为false表示 不能读空字符串。
     * 			
	 *	如果输入为空，或者输入大于limit的长度，就会提示重新输入。
     * @return
     */
    private static String readKeyBoard(int limit, boolean blankReturn) {
        
		//定义了字符串
		String line = "";

		//scanner.hasNextLine() 判断有没有下一行
        while (scanner.hasNextLine()) {
            line = scanner.nextLine();//读取这一行
           
			//如果line.length=0, 即用户没有输入任何内容，直接回车
			if (line.length() == 0) {
                if (blankReturn) return line;//如果blankReturn=true,可以返回空串
                else continue; //如果blankReturn=false,不接受空串，必须输入内容
            }

			//如果用户输入的内容大于了 limit，就提示重写输入  
			//如果用户如的内容 >0 <= limit ,我就接受
            if (line.length() < 1 || line.length() > limit) {
                System.out.print("输入长度（不能大于" + limit + "）错误，请重新输入：");
                continue;
            }
            break;
        }

        return line;
    }
}
```



