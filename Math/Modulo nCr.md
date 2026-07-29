``` java
//nCr
public long nCr(int n,int k){
        if(k<0 || k>n) return 0;

        k=Math.min(n-k,k);
        long num=1;
        long den=1;
        for(int i=1;i<=k;i++){
            num=num*(n-i+1)%MOD;
            den=den*i%MOD;
        }

        return num*power(den,MOD-2)%MOD;

}
//calculation of mod power in log(e)
public long power(long b,int e){
        long res=1;

        while(e>0){
            if((e&1)==1){
                res=(res * b)% MOD;
            }

            b=(b * b) % MOD;
            e>>=1;
        }

        return res;
}
```
