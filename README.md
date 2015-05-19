# wangdatou1000.github.io
##个人博测试，字符串匹配的sunday算法
``` java
package string;
/**
 * 功能描述：sunday字符串匹配算法，java实现。 1,Sunday算法是Daniel
 * M.Sunday于1990年提出的一种比BM算法搜索速度更快的算法。
 * 
 * 2,Sunday算法其实思想跟BM算法很相似，只不过Sunday算法是从前往后匹配， 在匹配失败时关注的是文本串中参加匹配的最末位字符的下一位字符。
 * 如果该字符没有在匹配串中出现则直接跳过，即移动步长= 匹配串长度+ 1；否则，同BM算法一样其移动步长=匹配串中最右端的该字符到末尾的距离+1。
 * 
 * @author 王世杰
 * @version 1.0, 2015年4月22日 下午2:38:26
 */
public class SundayForSubString {

	public static void main(String[] args) {

	}

	public int indexOf(String text, String pattern) {
		if (text == null || pattern == null)
			return -1;
		final int n = text.length();
		final int m = pattern.length();
		if (m > n || m == 0)
			return -1;
		int i = 0, j = 0;
		int ti = 0, tj = 0;
		final char[] t = text.toCharArray();
		final char[] p = pattern.toCharArray();
		while (i < n && j < m) {
			/* 先左对齐往右挨个比较，如果相同则比较下一个。 */
			if (t[i] == p[j]) {
				i++;
				j++;
			} else {
				/*
				 * 等出现不相同字符时，则将长字符串相对短标字符串尾部下一个字符与短标字符串比较， 比较顺序是从短标字符末尾开始往头逆序比较。
				 */
				ti = i + m - j;// 尾部的下一个字符为比较字符
				tj = m - 1;// 从尾部开始
				if (ti >= n)
					break;// 如果比较字符不存在，则结束比较。
				for (; tj >= 0 && t[ti] != p[tj]; tj--)
					;// 如果不相同就一直比较，直到相同为止。
				i = i - j + m - tj;// 设置字符串移动后的的位置，也就是j相对长的位置，
				j = 0;// 从短字符串头部开始比较
			}
			// 进行新一轮的比较
		}
		// 比较结束后，看j与m是否相等，相等则比较完成找到了字符串，并返回短字符串在长字符串中的起始位置，
		// 如果不相等则没有匹配到，返回-1。
		return j == m ? (i - j) : -1;
	}

}

```
