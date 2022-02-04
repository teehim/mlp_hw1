# BADS 7604 Group Assignment 1 (Group 4)
## 1. Dataset
Heart Attack Analysis & Prediction Dataset (Kaggle: https://www.kaggle.com/rashikrahmanpritom/heart-attack-analysis-prediction-dataset)

### Fields:
- Age : Age of the patient
- Sex : Sex of the patient
- exang: exercise induced angina (1 = yes; 0 = no)
- ca: number of major vessels (0-3)
- cp : Chest Pain type chest pain type
    - Value 1: typical angina
    - Value 2: atypical angina
    - Value 3: non-anginal pain
    - Value 4: asymptomatic
- trtbps : resting blood pressure (in mm Hg)
- chol : cholestoral in mg/dl fetched via BMI sensor
- fbs : (fasting blood sugar > 120 mg/dl) (1 = true; 0 = false)
- rest_ecg : resting electrocardiographic results
    - Value 0: normal
    - Value 1: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV)
    - Value 2: showing probable or definite left ventricular hypertrophy by Estes' criteria
- thalach : maximum heart rate achieved

### Label:
- target : 0=less chance of heart attack / 1=more chance of heart attack

## 2. Experiment Result
### We experiment on each hyperparameter with the following default hyperparameter (change each hyperparameter and keep the default for others) and evaluate the result using model accuracy on test set
- random state = 88
- number of hidden layer: 3
- number of neurons: 100 / 200 / 100
- dropout = 0.3
- activation function = relu / relu / relu / sigmoid
- learning rate = 0.001
- optimizer = Adam
- loss function = binary cross entropy
- batch size = 128
- epoch = 100

### Number of Hidden Layer & Neural
We choose **1 hidden layer with 512 neurons**

<img src="https://github.com/teehim/mlp_hw1/blob/main/images/result1.JPG?raw=true" style="width:500px;"/>

### Activation Function and Loss Function
Because in previous experiment we choose 1 hidden layer, therefore in this experiment we will experiment on a model with 1 hidden layer (512 neurons) to reduce the amount of experiment

We choose **relu** as activation function and **binary cross entropy** as loss function


<img src="https://github.com/teehim/mlp_hw1/blob/main/images/result5.JPG?raw=true" style="width:500px;"/>

### Learning rate and Activation function
We choose **Adamax** as activation function and leaning rate of **0.001**

<img src="https://github.com/teehim/mlp_hw1/blob/main/images/result2.JPG?raw=true" style="width:300px;"/>

### Batch size and Epoch
We choose **1000 epochs** and **batch size of 256**

<img src="https://github.com/teehim/mlp_hw1/blob/main/images/result3.JPG?raw=true" style="width:800px;"/>

## 3. Putting it all together
After we got the result of all experiment, We use the best hyperparameter of each experiment to construct the final model

with
- random state = 88
- number of hidden layer: 1
- number of neurons: 512
- dropout = 0.3
- activation function = relu / sigmoid
- learning rate = 0.001
- optimizer = Adamax
- loss function = binary cross entropy
- batch size = 256
- epoch = 1000

<img src="https://github.com/teehim/mlp_hw1/blob/main/images/result6.JPG?raw=true" style="width:500px;"/>

and get the following result
Accuracy: **0.84615**
Loss: **0.97997**

## 4. Traditional ML model
We choose 3 traditional ML model: Logistic Regression, Random Forest & KNN and get the following result

<img src="https://github.com/teehim/mlp_hw1/blob/main/images/result4.JPG?raw=true" style="width:300px;"/>

## 5. Comparison and Discussion
จากผลที่ได้จาก final model และ traditional ML model จะเห็นได้ว่าค่า Accuracy ที่ได้จาก final model นั้นต่ำกว่าผลที่ได้จาก knn model และผลที่ได้ระหว่างจากทดลองปรับเปลี่ยน hyperparameter ในบางรอบ

จึงสามารถสรุปได้ว่าการทดลองปรับ hyperparameter ด้วยการแยก hyperparameter แต่ล่ะตัวให้สมาชิกแต่ล่ะคนไปทดลองเพื่อหาค่าที่ได้ผลดีที่สุด แล้วนำค่าที่ได้นั้นมารวมกันเป็น model ไม่ได้ทำให้ได้ผลลัพธ์ที่ดีที่สุด ดังนั้นการปรับจูน hyperparameters ควรจะค่อยๆปรับค่าทั้งหมดไปพร้อมกันมากกว่า

และเนื่องจากจำนวนข้อมูลที่เรานำมาใช้ในการทดลองมีจำนวนไม่มาก ทำให้ผลลัพธ์ที่ได้มีประสิทธิภาพที่ไม่แตกต่างจาก traditional ML model ทั่วไป

## 6. Pros and Cons
เมื่อเทียบกับ traditional ML model แล้ว เราพบว่า MLP มีข้อดี และข้อเสียดังนี้

### Pros
- สามารถใช้ MLP กับปัญหาใดๆก็ได้ ที่มีข้อมูลที่เป็น tabular data ต่างจาก ML model ที่บาง model เช่น KNN หรือ Logistic Regression ที่ต้องวิเคราะห์ข้อมูลก่อนว่ามีการกระจายตัวที่เหมาะสมกับ model หรือไม่
- สามารถเพิ่ม-ลด ความซับซ้อนของ model ได้ด้วยการเพิ่ม-ลด จำนวนของ hidden layer และ neuron

### Cons
- ใช้เวลาในการ traing มากกว่า ML model ทำให้การปรับจูน hyperparameter นั้นใช้เวลามากกว่ามาก
- Black box issue: ไม่สามารถอธิบายผลลัพธ์ที่ model predict ออกมาได้ เมื่อเทียบกับ 
    - KNN ที่สามารถอธิบายได้ว่าเพราะเพื่อนบ้านส่วนใหญ่เป็น class นั้น
    - Logistic Regression ที่สามารถอธิบายได้ด้วยสมการที่ได้จากการ train model
    - Random Forest ที่สามารถบอก feature importance ได้
- เมื่อมีจำนวนข้อมูลไม่มาก ประสิทธิภาพที่ได้นั้นไม่แตกต่างกับ ML model แต่ต้องให้ทรัพยากรในการ train มากกว่า

## 7. Recommendations
- ไม่ควรจะแยกกันปรับจูน hyperparameter แล้วนำมารวมกัน เพราะไม่ได้ให้ผลลัพธ์ที่ดีที่สุด ควรจะแยกกันปรับทุกๆ hyperparameter แล้วเอาผลลัพธ์ที่ดีที่สุดมามากกว่า
- ถ้าหากข้อมูลที่มีจำนวนไม่มาก ควรใช้ traditional ML model เพราะใช้ทรัพยากรในการ train น้อยกว่า และสามารถอธิบายผลได้

## 8. Members
- (16.67%) 6220422048 กชกร เรืองศรี
- (16.67%) 6220422065 สุธาสินี โพธิ์แจ่ม  
- (16.67%) ไตรเทพ จันทร์เทพ
- (16.67%) 6310422028 วรเมธ ปลอดโปร่ง
- (16.67%) 6310422031 ธนัตถ์กรณ์ ชื่นบรรลือสุข
- (16.67%) 6310422046 วีระศักดิ์ การุณย์
