# 1.類型 
> String 字串 ("ABC", "abc")  
>Char 字符 ("A", "a")  
>Integer 整數 (132, 321)  
>Single 小數 (3.14, 2.72)  
>Boolean 布爾 (True/False)  

# 2.陣列(Array)
## 一維陣列

## 二維陣列
### 平行陣列


# 3.語法
```vbnet

Const
Dim

（string）.length 返回字串長度 (（"abc"）.Length = 3, （"ab c"）.Length) = 4)

Lcase(string)只有大寫字母被轉換為小寫；所有小寫字母和非字母字符保持不變。
UCase(string)只有小寫字母被轉換為大寫；所有大寫字母和非字母字符保持不變。

Val(string) 返回字串變量中的數字 *沒有數字返回0 (Val)"abc123" = 123,Val("abc") = 0) 
```
```vbnet
If （條件）Then *條件正確 
	（執行指令） 
Else *條件不正確 
	（執行指令） 
End if

For i (控制循環）= 數值變量 (始) To 數值變量（終) Step 數值變量（執行每一次i增加多少值） 
      （執行指令） 
Next*i 是否大於終 

Exit For(將控制轉移到For循環之外)

While （判斷是否符合條件） *符合條件 
      （執行指令） 
End While *不符合條件 

Do 
	(執行指令)
Loop Until（條件）*符合條件 
*不符合條件 
(執行指令)

ByVal 按值傳遞
ByRef 按址傳遞

Return（返回內容）

Sub(過程名）（ByVal/ByRef （變量名）As (變量種類）*每個變量名要建立一次 用"，"分） 
	（語句） 
End Sub 

Function （過程名）（ByVal/ByRef （變量名）as（變量種類）*每個變量名要建立一次）As(返回值類型） 
      （數學運算） 
End Function  

```
# 4.運算符
|  | 1 + 1 = 1 | 1 + 1 = 2 | |
|--|--|--|--
| And|False |True |False |
|Or |False  |True|True||
```vbnet
/ 除法 (3 / 5 = 0.6, 3 / 6 = 0.5 , 35 / 3 = 11.666)
\ 整數除法（取商）(35 \ 3 = 11 ,
Mod 模數（取餘數）(35 Mod 3 = 2 ,

= 等於 (1=2 = False, 1=1 = True)
<> 不等於 (1<>2 = True, 1<>1 =False)

>	大於（A>B = False , 2 > 1 True)
<	小於（A<B = True , 2 < 1 False)
```
## ASCII(美國標準資訊交換碼)
|十進制|圖形|十進制|圖形
|--|--|--|--|
|65|A|98|a|
|66|B|99|b|
|67|C|100|c|

[**wiki**](https://zh.m.wikipedia.org/zh-hk/ASCII#%E5%8F%AF%E6%98%BE%E7%A4%BA%E5%AD%97%E7%AC%A6)

# 5.文件I/O

> Dim 變量名 As IO.SteamReader = IO.File.openText("文件路徑")
變量名.ReadLine()


```vbnet
Module Read_data_from_a_text_file

    Sub Main()
        Const filepath As String = "C:\sur\t\t"
        Const filename As String = "example2.txt"
        Dim sr As IO.StreamReader = IO.File.OpenText(filepath & filename)
        Dim line_string As String

        '讀取文字檔的第一行。
        line_string = sr.ReadLine()

        '檢查從文字檔讀取的字串是否 nothing，
        '從而檢查是否已到達檔尾。
        While line_string <> Nothing
            Console.WriteLine(line_string)
            line_string = sr.ReadLine()
        End While

        sr.Close()
    End Sub

End Module
```

> Dim 變量名 As IO.StreamWriter = IO.File.CreateText("文件路徑")
> 變量名.WriteLine(" ")

```vbnet
Module Write_10_lines_to_a_text_file

    Sub Main()
        Const filepath As String = "C:\"
        Const filename As String = "example2.txt"
        Dim sw As IO.StreamWriter = IO.File.CreateText(filepath & filename)
        Dim i As Integer
        Dim sentence As String

        For i = 1 To 10
            sentence = "This is line no. " & Str(i).Trim
            sw.WriteLine(sentence)
        Next

        sw.Close()
    End Sub

End Module
```
> 變量名.Close()  關閉文件

# 6.檢索
## 順序檢索(線性搜索）

> 從頭找到尾   
> **好處**：適用性最廣  
> **壞處**：速度最慢  

## 對分檢索(二分搜尋演算法)

> **好處**:如果中間元素正好是要搜尋的元素，則搜尋過程結束。每一次比較都使搜尋範圍縮小一半。   
> **壞處**:陣列必須事先被排序。  
> 
![请添加图片描述](https://img-blog.csdnimg.cn/64ae68fce1bb44339f1f1690e61bde3c.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/ac8e272810bd41908fbe2378eb5db4ca.jpeg#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/4feb823d53a74ef69850cdfd7f902dd3.jpeg#pic_center)
```vbnet
Module Binary_search
    Sub Main()
        Dim alphabet_list() As Char = {"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", _
                                       "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", _
                                       "U", "V", "W", "X", "Y", "Z"}
        Dim pass, first, last, middle, location_found As Integer
        Dim target_alphabet As Char
        Dim target_found As Boolean

        Console.Write("Enter an alphabet to search: ")
        target_alphabet = Console.ReadLine()

        pass = 0
        first = 0
        last = alphabet_list.GetUpperBound(0)
        target_found = False

        While (first <= last) And Not target_found
            pass += 1
            middle = (first + last) \ 2
            Console.WriteLine("Pass " & pass & " " & middle & " " & alphabet_list(middle))
            If target_alphabet = alphabet_list(middle) Then
                location_found = middle + 1 '在 VB，於列表內的位置是 索引 + 1
                target_found = True
            Else
                If target_alphabet < alphabet_list(middle) Then
                    last = middle - 1
                Else
                    first = middle + 1
                End If
            End If
        End While

        If target_found Then
            Console.WriteLine(target_alphabet & " found at loaction " & location_found)
        Else
            Console.WriteLine(target_alphabet & " is not found in the list.")
        End If
    End Sub
End Module
```
# 7.排序
## 快速排序
>  1. 挑選基準值：從數列中挑出一個元素，稱為「基準」（pivot），
>  
>  2. 分割：重新排序數列，所有比基準值小的元素擺放在基準前面，所有比基準值大的元素擺在基準後面（與基準值相等的數可以到任何一邊）。在這個分割結束之後，對基準值的排序就已經完成，
>  
>  3. 遞歸排序子序列：遞歸地將小於基準值元素的子序列和大於基準值元素的子序列排序。
>  
> 遞歸到最底部的判斷條件是數列的大小是零或一，此時該數列顯然已經有序。

![请添加图片描述](https://img-blog.csdnimg.cn/cb7e4a980a074d4bb1e442ed02b2eb16.gif)![请添加图片描述](https://img-blog.csdnimg.cn/7c53d4c0e23344a3b21f70b8abbd2c6d.gif)

## 合併排序(歸併排序)

![请添加图片描述](https://img-blog.csdnimg.cn/dc0f17c7516444439e28efced13063b9.gif)
```vbnet
Module Merge_sort
    Sub Display_integer_array(ByVal x() As Integer)
        Dim i As Integer
        For i = 0 To x.GetUpperBound(0)
            Console.Write(x(i) & "  ")
        Next
        Console.WriteLine()
    End Sub

    Sub Merge_two_lists(ByRef array() As Integer, 
                        ByVal left As Integer, 
                        ByVal mid_point As Integer, 
                        ByVal right As Integer)

        Dim x_marker, y_marker, z_marker As Integer

        '說明一個臨時陣列儲存
        '較低端和較高端的子陣列
        Dim z(right) As Integer

        x_marker = left
        y_marker = mid_point
        z_marker = left

        '掃瞄較低端和較高端的子陣列
        '並比較它們的元素的值，
        '把較小的元素賦值至臨時陣列
        While x_marker < mid_point And y_marker < right
            If array(x_marker) <= array(y_marker) Then
                z(z_marker) = array(x_marker)
                x_marker += 1
            Else
                z(z_marker) = array(y_marker)
                y_marker += 1
            End If
            z_marker = z_marker + 1
        End While

        '把較低端的子陣列餘下的元素
        '複製至臨時陣列
        While x_marker < mid_point
            z(z_marker) = array(x_marker)
            x_marker = x_marker + 1
            z_marker = z_marker + 1
        End While

        '把較高端的子陣列餘下的元素
        '複製至臨時陣列
        While y_marker < right
            z(z_marker) = array(y_marker)
            y_marker = y_marker + 1
            z_marker = z_marker + 1
        End While

        '把臨時陣列的元素複製至陣列
        For z_marker = left To right - 1
            array(z_marker) = z(z_marker)
        Next
    End Sub

    Sub Merge_sort_procedure(ByRef array() As Integer, _
                             ByVal left As Integer, ByVal right As Integer)
        Dim mid_point As Integer

        '測試子陣列是否有超過 1 個元素
        If left < right Then
            '利用整數除法計算把陣列分割為
            '兩個大小相若的子陣列的中點
            '(避免若陣列大小是奇數時出現小數位)
            mid_point = (left + right) \ 2

            '遞歸地調用 Merge_sort_procedure 來把
            '較低端的分區排序
            Merge_sort_procedure(array, left, mid_point)

            '遞歸地調用 Merge_sort_procedure 來把
            '較高端的分區排序
            Merge_sort_procedure(array, mid_point + 1, right)

            '合併兩個已排序的子列表
            Merge_two_lists(array, left, mid_point + 1, right + 1)
        End If

        Display_integer_array(array)
    End Sub

    Sub Main()
        Dim x() As Integer = {7, 5, 1, 8, 9, 3, 4}

        Merge_sort_procedure(x, x.GetLowerBound(0), x.GetUpperBound(0))
    End Sub

End Module
```
## 冒泡排序

> 1. 比較相鄰的元素。如果第一個比第二個大，就交換它們兩個。
> 
> 2. 對每一對相鄰元素作對比。*從開始第一對到結尾的最後一對*
> （這步做完後，最後的元素會是最大的數。）
> 
>  3. 針對所有的元素重複以上的步驟，除了最後一個。
>  
>  4. 持續每次對越來越少的元素重複上面的步驟，直到沒有任何一對數字需要比較。


![请添加图片描述](https://img-blog.csdnimg.cn/accb6ef5d484444cb03db6644b52eb7d.gif)

```vbnet
Module Bubble_sort
    Sub Swap_integer(ByRef x As Integer, ByRef y As Integer)
        Dim temp As Integer
        temp = y
        y = x
        x = temp
    End Sub

    Sub Main()
        Dim X() As Integer = {5, 8, 4, 10, 2}
        Dim i, j, k, N As Integer

        N = X.GetUpperBound(0) + 1 '在 VB，陣列的大小 = 上界 + 1

        '顯示原本未排序的陣列。
        Console.Write("Initial: ")
        For k = 0 To N - 1
            Console.Write(X(k) & "  ")
        Next
        Console.WriteLine()

        For j = 1 To N - 1
            Console.Write("Pass {0} : ", j)
            For i = 1 To N - j
                '在 VB，陣列下界的下標由 0 開始
                '所以，用 X(i - 1) > X(i) 作比較
                '而不是 X(i) > X(i + 1)
                If X(i - 1) > X(i) Then
                    Swap_integer(X(i - 1), X(i))
                End If
            Next

            '於每遍後，顯示陣列。
            For k = 0 To N - 1
                Console.Write(X(k) & "  ")
            Next
            Console.WriteLine()
        Next
    End Sub
End Module
```
## 插入排序

> 在已排序序列中**從後向前**掃描，找到相應位置並插入。
> 在從後向前掃描過程中，需要反覆把已排序元素逐步向後挪位，為最新元素提供插入空間。

![请添加图片描述](https://img-blog.csdnimg.cn/f2e0cf70663c46d2a376b48bed27c75f.gif)
# 8.數據結構
## 堆疊(stack)

> **推入**(push)：將資料放入堆疊頂端，堆疊頂端移到新放入的資料。
> **彈出**(pop)：將堆疊頂端資料匯出，堆疊頂端移到移除後的下一筆資料。
> 先入後出，後入先出（*LIFO*, Last In First Out） 的原理運作
除頭尾節點之外，每個元素有一個前驅，一個後繼。

![请添加图片描述](https://img-blog.csdnimg.cn/56bb9e6c050f4786b02d22caa84c725a.png)
## 隊列(queue）

> 先入先出，後入後出（*FIFO*, first in first out） 的原理運作
> 同現實中的排隊一樣

![请添加图片描述](https://img-blog.csdnimg.cn/cb6225f2d9664173a3067fba36eb471f.png)
## 鏈表（鏈結串列）
