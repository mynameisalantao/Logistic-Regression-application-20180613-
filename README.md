機器學習Logistic Regression應用(20180613)
==============================================
程式語言:使用matlab ，撰寫:Alan Tao<br />
因為這有許多矩陣運算，用c++不太方便，加上希望能夠看到圖，能顯現出結果，所以改用matlab<br />
首先假設training data

<pre><code>training_input=[1,3,5,3,16,19,23,20;2,1,3,4,19,28,14,20];
training_output=[1,1,1,1,0,0,0,0];</pre></code>
共有8筆資料，將資料都寫入矩陣中
<pre><code>| 1  3  5  5  16  19  23  20  |
| 2  1  3  4  19  28  14  20  |
| 1  1  1  1   0   0   0   0  |</pre></code>
矩陣training_input的行向量即為每筆training data的2個feature<br />
而陣列training_output則紀錄屬於class1還是class2<br />
若為class1，則其元素值為1，反之則為0<br />
接著定義function
<pre><code>function f = probability_function(x,w,b)
z=dot(x,w)+b;
f=1/(1+exp(-z));  
end</pre></code>
輸入training data x,向量w與常數b<br />
可以得到P(class1|x)<br />
也就是向量x是在class1的機率<br />
接著給訂初值
<pre><code>b=10;
w=[0.01;0.01];
learning_rate1=0.001;
learning_rate2=0.001;</pre></code>
接著是主程式部分
<pre><code>for k=1:1:400
     for j=1:1:2
         sigma1=0;
         sigma2=0;
         for i=1:1:8
              sigma1=sigma1-(training_output(i)-probability_function(training_input(:,i),w,b))*training_input(j,i);
              sigma2=sigma2-(training_output(i)-probability_function(training_input(:,i),w,b));
         end
         w(j,1)=w(j,1)-learning_rate1*sigma1;  
         b=b-learning_rate2*sigma2;        
 end
 
 subplot(2,1,1);
 plot(k,sigma1,'r+-.');
     hold on;
     subplot(2,1,2);
     plot(k,sigma2,'r+-.');
     hold on;
 end</pre></code>
 
 ![Imgur](https://i.imgur.com/UJ0tfYu.png)
 
 最後可以檢查分界線在以2個feature為軸的平面上
 <pre><code>for i=0:0.01:30
    for j=0:0.01:30
        a=probability_function([i;j],w,b);
        if a<=0.51&&a>=0.49
        plot(i,j,'r+-.');
        hold on;
        end
    end
end</pre></code>

![Imgur](https://i.imgur.com/RSIHfZe.png)
