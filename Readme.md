## ������ 1. �������� ��������

## ��������
��� ������� ��������� ������ �� �������������� ���������� � ����� �������� �����������. �� ������� ���������, ������� ���������� **25** ����� �������� **30'000** ��������, ������� ������� �� �������� **'a'** � **'b'**.

��� ������ ������ �� ����� ����� ������ ����������� ����������, ���������� �� ����� �������� 'a'. �.�., ��������, ��� ������ "aaababbaaaaabaa" ������� ����� ����� 5 (5 �������� 'a' ������). ��� ����� �� ������� ����� ������������� ��������, ������� ���������� ������������ ������� �������������� ������ ����� ���������� � ������������ ������� �����, ����� ���� ��������� ���� �� ����� ���� ������ 'b'. ���� ������ 'b' �� ��� ������, �� ��������� ���������� ������ ����� ����������, ���� �� �������� ������������. **������ ���� �������� ��� ������.**

� ����� �� ������� ��������� ���:
```java
import java.util.*;

public class Main {

    public static void main(String[] args) throws InterruptedException {
        String[] texts = new String[25];
        for (int i = 0; i < texts.length; i++) {
            texts[i] = generateText("aab", 30_000);
        }

        long startTs = System.currentTimeMillis(); // start time
        for (String text : texts) {
            int maxSize = 0;
            for (int i = 0; i < text.length(); i++) {
                for (int j = 0; j < text.length(); j++) {
                    if (i >= j) {
                        continue;
                    }
                    boolean bFound = false;
                    for (int k = i; k < j; k++) {
                        if (text.charAt(k) == 'b') {
                            bFound = true;
                            break;
                        }
                    }
                    if (!bFound && maxSize < j - i) {
                        maxSize = j - i;
                    }
                }
            }
            System.out.println(text.substring(0, 100) + " -> " + maxSize);
        }
        long endTs = System.currentTimeMillis(); // end time

        System.out.println("Time: " + (endTs - startTs) + "ms");
    }

    public static String generateText(String letters, int length) {
        Random random = new Random();
        StringBuilder text = new StringBuilder();
        for (int i = 0; i < length; i++) {
            text.append(letters.charAt(random.nextInt(letters.length())));
        }
        return text.toString();
    }
}
```
���������� ��� ��������� ���� � ������, ���������. ��������� �������� ������� ���������, **���� ������ - �������� � ���������� �������������� ����������������**.

## ����������
1. ���������� ��������� ������ ������ �� ������� `texts` � ��������� ������.
2. �� ����� �������� `List<Thread> threads`, ��� �������� ����������� �������.
3. ����� ���������� ����� `new Thread(...)`, � ������������ ��������� ���������� ������� ���������� `Runnable`, � ������� ����� ���������� ������ ��������.
4. �� �������� �� ������ �������� ��������� ������ ������ � ������ �������, �� � ��������� �����.
5. ����� ����� ������� �������� ���������� ������� �������� ������� ���������:
  ```java
   for (Thread thread : threads) {
       thread.join(); // ��������, ��� ����� ����� ������ �������� ����� � thread ����������
   }
   ```
�� ��������� ��� ���������, ��������� � �������� ������. � �������� ������� �� �������� ��������� ������ �� ����������� � ��������.
