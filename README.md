機器學習Logistic Regression應用(20180613)
==============================================
因為這有許多矩陣運算，用c++不太方便，加上希望能夠看到圖，能顯現出結果，所以改用matlab<br />
首先假設training data
>training_input=[1,3,5,3,16,19,23,20;2,1,3,4,19,28,14,20];
>training_output=[1,1,1,1,0,0,0,0];
共有8筆資料，將資料都寫入矩陣中<br />
| 1  3  5  5  16  19  23  20  |<br />
| 2  1  3  4  19  28  14  20  |<br />
<br />
| 1  1  1  1   0   0   0   0  |<br />
矩陣training_input的行向量即為每筆training data的2個feature<br />
而陣列training_output則紀錄屬於class1還是class2<br />
若為class1，則其元素值為1，反之則為0<br />
接著定義function<br />
>function f = probability_function(x,w,b)
>z=dot(x,w)+b;
>f=1/(1+exp(-z));
>end
