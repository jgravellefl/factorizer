import java.util.ArrayList;
import java.util.Scanner;

public class factoring {
    public static void factorize(int a, int b, int c){
        int origB = b;
        char aSign = '+';
        char cSign = '+';
        if (a < 0){
            a *= -1;
            aSign = '-';
        }
        if (b < 0){
            b *= -1;
        }
        if (c < 0){
            c *= -1;
            cSign = '-';
        }
        int min = a;
        if (b < min){
            min = b;
        }
        if (c < min){
            min = c;
        }
        int commonFactor = 0;
        for (int i = 1; i < min + 1; i++){
            if (a % i == 0 && b % i == 0 && c % i == 0 ){
                commonFactor = i;
                a /= i;
                b /= i;
                c /= i;
            }
        }
        System.out.println("common factor" + commonFactor);

        ArrayList<Integer> factorsa = new ArrayList<>();
        ArrayList<Integer> factorsb = new ArrayList<>();
        for (int i = a; i > 0; i-- ){
            for (int n = i; n > 0; n--){
                if (i * n == a){
                    if (aSign == '+') {
                        factorsa.add(n);
                        factorsa.add(i);
                    }
                    else {
                        factorsa.add(n);
                        factorsa.add(i * -1);
                        factorsa.add(n * -1);
                        factorsa.add(i);
                    }
                }
            }
        }
        for (int i = c; i > 0; i--){
            for (int n = i; n > 0; n--){
                if (i * n == c){
                    if (cSign == '+') {
                        factorsb.add(n);
                        factorsb.add(i);
                    }
                    else{
                        factorsb.add(n);
                        factorsb.add(i * -1);
                        factorsb.add(n * -1);
                        factorsb.add(i);
                    }
                }
            }
        }
        b = origB / commonFactor;
        System.out.println(factorsa);
        System.out.println(factorsb);
        int factorCounter = 0;
        for(int i = 0; i < factorsa.size(); i += 2){
            for(int n = 0; n < factorsb.size(); n += 2){
                if(factorsa.get(i) * factorsb.get(n) + factorsa.get(i+1) * factorsb.get(n+1) == b) {
                    System.out.println("Factors found!");
                    System.out.println( ""+ commonFactor + "(" + factorsa.get(i) + "x + " + factorsb.get(n+1) + ") " + "(" +  factorsa.get(i+1) + "x + " + factorsb.get(n) + ")");
                    factorCounter++;
                }
                else if (factorsa.get(i) * factorsb.get(n+1) + factorsa.get(i+1) * factorsb.get(n) == b){
                    System.out.println("Factors found!");
                    System.out.println( "" + commonFactor + "(" + factorsa.get(i) + "x + " + factorsb.get(n) + ")" + "(" + factorsa.get(i+1) + "x + " + factorsb.get(n+1) + ")");
                    factorCounter++;
                }
            }
        }
        if (factorCounter == 0){
            System.out.println("No factors found");
        }

    }
    public static void main(String[] args){
        System.out.println("input numbers with a space in between");
        Scanner scnr = new Scanner(System.in);
        int x = scnr.nextInt();
        int y = scnr.nextInt();
        int z = scnr.nextInt();
        factorize(x, y, z);

    }
}

