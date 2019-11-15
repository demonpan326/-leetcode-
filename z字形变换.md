z字形变换：

第一种方法：

按行考虑，每一行有一定的规律。

例如：4行的话，第一行与最后一行每次下标都加2*(numRows-1)，也就是6

第二行的话，先是4，后是2；第三行的话，先是2，后是4，循环。

第二种方法:

建立numrows大小的字符串列表，遍历字符串，加入到对应的字符串列表里面。

所以最终的代码如下所示：

# 代码一：

```python
class Solution(object):
    def convert(self, s, numRows):
        string=''
        size=len(s)
        j=0
        if (numRows==1):#单独考虑行数为1的情况
            return s
        for i in range(1,numRows+1):
            j=i-1
            k=0 #这个不能放在外层循环外，因为不确定每层结束后，k的值一定为0
            while j<size :
                string+=s[j]
                if(i==1 or i==numRows):#注意i代表层数
                    j += 2*(numRows-1)
                elif(k==0):
                    j += 2*(numRows-i)
                    k=1
                else:
                    j +=abs( 2*(numRows-1)-2*(numRows-i))#注意绝对值
                    k=0

        return string
```



# 代码二：

```python
class Solution(object):
    def convert(self, s, numRows):
        size=len(s)
        direction=-1
        string=[]
        str=''
        for i in range(min(size,numRows)):
            string.append('')
        j=0
        for i in range(size):
            if(direction==-1):
                string[j]+=s[i]
                j+=1
            else:
                string[j]+=s[i]
                j-=1
            if (j==numRows):
                direction=1
                j=j-2
            elif(j==-1):
                direction=-1
                j=j+2
        for i in range(len(string)):
            str+=string[i]
        return str
```

