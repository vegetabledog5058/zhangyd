# LeetCode(从0-1)

## 一.交替合并字符串

1.双指针和stringBuilder(官方)

```java
public static String relete2(String word1, String word2) {
        StringBuilder sb = new StringBuilder();
        int l1 = word1.length(),l2 = word2.length();
        int i = 0, j = 0;
        while(i<l1||j<l2){
            if(i<l1){
                sb.append(word1.charAt(i));
                i++;
            }
            if(j<l2){
                sb.append(word2.charAt(j));
                j++;
            }
        }
        return sb.toString();

    }
```

2.转换成为字符数组后循环拼接

```java
public static String relete1(String word1, String word2) {
        char arr1[] = word1.toCharArray();
        char arr2[] = word2.toCharArray();
        String str = "";
        char[] bigger = arr1.length > arr2.length ? arr1 : arr2;
        char[] smaller = arr1.length > arr2.length ? arr2 : arr1;
        for (int i = 0; i < bigger.length; i++) {

            if (i < smaller.length) {
                str = str + arr1[i] + arr2[i];
            } else {
                str = str + bigger[i];
            }
        }
        return str;

    }
```

## 二.找不同

1.