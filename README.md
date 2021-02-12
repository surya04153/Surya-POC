# Surya-POC
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;


class Result {

    /*
     * Complete the 'maxPoints' function below.
     *
     * The function is expected to return a LONG_INTEGER.
     * The function accepts INTEGER_ARRAY elements as parameter.
     */

    public static long maxPoints(List<Integer> nums) {
        int n= nums.size();
        int l=1;int r=1;
    int mx = 0, k; 
     // find maximum element of the array. 
     for (int i = 0; i < n; ++i) 
         mx = Math.max(mx, nums.get(i)); 
  
     // initialize count of all elements to zero. 
     int[] count = new int[mx + 1]; 
     for(int i = 0; i < count.length; i++) 
         count[i] = 0; 
  
     // calculate frequency of all elements of array. 
     for (int i = 0; i < n; i++) 
         count[nums.get(i)]++; 
  
     // stores cost of deleted elements. 
     int[] res = new int[mx + 1]; 
     res[0] = 0; 
  
     // selecting minimum range from L and R. 
     l = Math.min(l, r); 
  
     for (int num = 1; num <= mx; num++) { 
  
         // finds upto which elements are to be 
         // deleted when element num is selected. 
         k = Math.max(num - l - 1, 0); 
  
         // get maximum when selecting element num or not. 
         res[num] = Math.max(res[num - 1], num * count[num] + res[k]); 
     } 
  System.out.println(res[mx]);
     return res[mx]; 

    }

}
public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int elementsCount = Integer.parseInt(bufferedReader.readLine().trim());

        List<Integer> elements = IntStream.range(0, elementsCount).mapToObj(i -> {
            try {
                return bufferedReader.readLine().replaceAll("\\s+$", "");
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        })
            .map(String::trim)
            .map(Integer::parseInt)
            .collect(toList());

        long result = Result.maxPoints(elements);
        

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}

