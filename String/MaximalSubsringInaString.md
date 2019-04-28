Maximal Subsring In a String


```java 
class Solution {
  public static void main(String[] args) {
    
    String str1 = "My name is Jason";
                                    
    // System.out.println(xxxx(str1)); // log: Jason
    String sens = "you and me";
                      // r
                   // l
    
    System.out.println(longestWord(sens)); // log: Jason
  }
  
  public static String longestWord(String sens) {
    int l = -1, r = 0;
    
    String res = "";
      
    while(r < sens.length()){
      if(sens.charAt(r) == ' ') {
        String tmp = sens.substring(l + 1, r);
        // check if need to update res
        if(tmp.length() > res.length()){
          res = tmp;
        }
        // update l
        l = r; 
      }
      r++;
    }
    
    // r == sens.length();
    // l == last space
    String last = sens.substring(l, r);
    if(last.length() > res.length()){
      res = last;
    }
    
    return res;
  }
}

```
