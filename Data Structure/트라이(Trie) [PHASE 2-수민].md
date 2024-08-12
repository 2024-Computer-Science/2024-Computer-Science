<aside>
💡 문자열에서 검색을 빠르게 도와주는 자료구조이다.

</aside>

- 정수형에서 이진 탐색트리를 이용하면 시간 복잡도가 O(logN)이지만, 문자열에 적용하면 문자열의 최대 길이(M)에 따라 O(M*logN)이 된다.
- 트라이를 활용하면 O(M)만에 검색이 가능해진다.

### 👩🏻‍💻 백준 5052 전화번호목록

[](https://www.acmicpc.net/problem/5052)

- 긴급전화: 911
- 상근: 97 625 999
- 선영: 91 12 54 26
    
![image](https://github.com/user-attachments/assets/40deca31-d2b6-4746-a08b-63dddabc4132)

![image](https://github.com/user-attachments/assets/89018fed-b3ab-4568-9a7a-13bda8378c9f)

![image](https://github.com/user-attachments/assets/a4fe9abd-8ee4-42ca-be9e-197a4fd829ad)

이럴경우 911 누르면 긴급전화걸려서 선영이한테 전화를 못함 → NO

```sql
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class p5052 {
    public static class Trie {
        Trie[] child;
        boolean pass;
        boolean end;
        Trie() {
            child = new Trie[10];
            pass = false;
            end = false;
        }

        public boolean insert(String str, int idx) {
            //지금까지 같은데 나보다 짧은애가 있으면 안됨
            if(end) return false;

            //나 끝났는데 나보다 더 긴애가 있으면 안됨
            if(idx == str.length()) {
                end = true;
                return !pass;
            }
            else {
                int next = str.charAt(idx)- '0';
                if(child[next] == null) {
                    child[next] = new Trie();
                }
                pass = true;
                return child[next].insert(str, idx+1);
            }
        }
    }
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());

        for (int T = 0; T < t; T++) {
            int n = Integer.parseInt(br.readLine());
            boolean check = true;
            Trie trie = new Trie();

            for(int i=0;i<n;i++) {
                if(check)
                    check = trie.insert(br.readLine(),0);
                else br.readLine(); //이미 틀려먹었어도 readLine해줘야됨
            }

            if(check) System.out.println("YES");
            else System.out.println("NO");
        }
    }

}

```
