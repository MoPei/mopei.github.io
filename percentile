# Percentile 百分位数
在日常教学应用中, 百分位数就是: 有百分之多少的人考的比你差.

"Order statistics provide a way of estimating proportions of the data that should fall above and below a given value, called a percentile. The pth percentile is a value, Y(p), such that at most (100p)% of the measurements are less than this value and at most 100(1- p)% are greater. The 50th percentile is called the median."

1. 计算百分位数

简单的计算: 考的差的学生/总学生数目

作为统计用, 且假设不会有大规模数据重复.

1. Step 1

Sort the data set so measurements are in order from lowest to highest. Normally this is done by entering the numbers in a computer spread sheet and then clicking on the sort command. You can do this manually by listing the possible measurements in order and then making a hash mark beside the appropriate number for each individual measurement.

2. Step 2

Start to calculate the percentile of an individual measurement (as an example we’ll assume this is a test score of 87 out of a possible 100) in a data set of 150. The formula to use is L/N(100) = P where L is the number of measurements less than 87, N is the total number of measurements in the data set (here 150) and P is the percentile. Count up the total number of measurements that are less than 87. We’ll assume this total is 113. This gives us L = 113 and N = 150.

3. Step 3

Divide out L/N to get the decimal equivalent. (113/150 = 0.753). Multiply this by 100 (0.753(100) = 75.3).

4. Step 4

Discard the digits to the right of the decimal point. For 75.3 this leaves 75. This is the percentile of a measurement of 87 in our example and means this measurement is higher than 75 percent of all the measurements in the data set.

更细致的计算方式, 可参考下文WikiPedia地址. 

 

1. 给定百分位数, 求解成绩
ETS明确规定Percentile是一定要求的一个统计量，不知道有没有G友遇到过关于Percentile的数学题，因为Percentile的计算比较复杂，所以我在此对Percentile的求法详述，以方便G友：
Percentile: percent below用概念来说没什么用，而且易让人糊涂，所以在此我归纳出一个公式以供G友参考。
设一个序列供有n个数，要求（k%）的Percentile：
（1）从小到大排序，求(n-1)*k%，记整数部分为i，小数部分为j
（2）所求结果＝（1－j）*第(i＋1)个数＋j*第(i+2)个数
特别注意以下两种最可能考的情况：
（1）j为0，即(n-1)*k%恰为整数，则结果恰为第(i+1)个数
（2）第(i+1)个数与第(i+2)个数相等，不用算也知道正是这两个数。
注意：我前面提到的Quartile也可用这种方法计算，
其中1st Quartile的k%=25%
2nd Quartile的k%=50%
3rd Quartile的k%=75%
计算结果一样。
例：（注意一定要先从小到大排序的，这里已经排过序啦！）
｛1，3，4，5，6，7，8，9，19，29，39，49，59，69，79，80｝共16个样本
（1）30%：(16-1)*30%=4.5=4+0.5
(1-0.5)*第5个数＋0.5*第6个数=0.5*6+0.5*7=6.5
（2）75%：15*75%=11.25=11+0.25 （3rd Quartile)
(1-0.25)*第12个数+0.25*第13个数=0.75*59+0.25*69＝51.5

```java
public static double percentile(List<Double> data, double p) {
    if (data == null || data.size() == 0) {
        throw new IllegalArgumentException("data collection is empty");
    }
    if (p <= 0 || p > 1) {
        throw new IllegalArgumentException("percent value range must in (0,1]");
    }
    data = data.stream().filter(Objects::nonNull).sorted(Double::compareTo).collect(Collectors.toList());

    int n = data.size();
    double px = p * (n - 1);
    int i = (int) Math.floor(px);
    double g = px - i;
    
    double result = 0;
    if (g == 0) {
        result = data.get(i);
    } else {
        result = (1 - g) * data.get(i) + g * data.get(i + 1);
    }
    
    return result;
}

```

原文引自：
http://forum.chasedream.com/dispbbs.asp?BoardID=22&id=233

另: 参考资料:

WikiPedia: http://en.wikipedia.org/wiki/Percentile – 偏重统计学

美国国家标准及技术研究所 http://www.itl.nist.gov/div898/handbook/prc/section2/prc252.htm 

How to Calculate Percentiles: http://www.ehow.com/how_2310404_calculate-percentiles.html
