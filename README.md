機器學習Logistic Regression應用(20180613)
==============================================
程式語言:使用matlab 撰寫:Alan Tao
因為這有許多矩陣運算，用c++不太方便，加上希望能夠看到圖，能顯現出結果，所以改用matlab<br />
首先假設training data<br />

training_input=[1,3,5,3,16,19,23,20;2,1,3,4,19,28,14,20];<br />
training_output=[1,1,1,1,0,0,0,0];<br />
共有8筆資料，將資料都寫入矩陣中<br />
| 1  3  5  5  16  19  23  20  |<br />
| 2  1  3  4  19  28  14  20  |<br />
| 1  1  1  1   0   0   0   0  |<br />
矩陣training_input的行向量即為每筆training data的2個feature<br />
而陣列training_output則紀錄屬於class1還是class2<br />
若為class1，則其元素值為1，反之則為0<br />
接著定義function<br />
function f = probability_function(x,w,b)<br />
z=dot(x,w)+b;<br />
f=1/(1+exp(-z));  <br />
end<br />
輸入training data x,向量w與常數b<br />
可以得到P(class1|x)<br />
也就是向量x是在class1的機率<br />
接著給訂初值<br />
b=10;<br />
w=[0.01;0.01];<br />
learning_rate1=0.001;<br />
learning_rate2=0.001;<br />
接著是主程式部分<br />
for k=1:1:400<br />
     for j=1:1:2<br />
         sigma1=0;<br />
         sigma2=0;<br />
         for i=1:1:8<br />
              sigma1=sigma1-(training_output(i)-probability_function(training_input(:,i),w,b))*training_input(j,i);<br />
              sigma2=sigma2-(training_output(i)-probability_function(training_input(:,i),w,b));<br />
         end<br />
         w(j,1)=w(j,1)-learning_rate1*sigma1;   <br />
         b=b-learning_rate2*sigma2;<br />
         
 end<br />
     
 subplot(2,1,1);<br /><br />
 plot(k,sigma1,'r+-.');<br />
     hold on;<br />
     subplot(2,1,2);<br />
     plot(k,sigma2,'r+-.');<br />
     hold on;<br />
 end<br />
 
 ![Imgur](https://i.imgur.com/UJ0tfYu.png)
 
 最後可以檢查分界線在以2個feature為軸的平面上<br />
 for i=0:0.01:30<br />
    for j=0:0.01:30<br />
        a=probability_function([i;j],w,b);<br />
        if a<=0.51&&a>=0.49<br />
        plot(i,j,'r+-.');<br />
        hold on;<br />
        end<br />
    end<br />
end<br />

![Imgur](https://i.imgur.com/RSIHfZe.png)
