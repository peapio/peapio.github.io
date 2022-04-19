# 连续序列的最大子列和


# 连续序列的最大子列和

给定N个整数的序列${A_1,A_2,\cdots,A_N}$

求函数$f(i,j)=max{0,\sum_{k=i}^nA_n},k=i$的最大值

```c
#include <stdio.h>
int MaxSub(int a[],int n){
	int i;
	int sum=0,maxsum=0;
	for (i=0;i<n;i++){
		sum+=a[i];
		if(sum>maxsum)
			maxsum=sum;
		else if(sum<0)
			sum=0;
	}
	return maxsum;
} 

int main(){
	int a[9] = {1,2,3,4,5,6,7,8,9};
	int max = MaxSub(a,9);
	printf("%d",max);
	return 0;
}
```

最优算法，时间复杂度为$O_{(n)}$

从头开始，加和小于零置零，确保抛弃段每一段都不可能增加后面最大值

## 分而治之

折半处理

再次化简$\Rightarrow NO_{(1)} + O_{nlog_n}$

最后时间复杂度就是$O_{nlog_n}$


