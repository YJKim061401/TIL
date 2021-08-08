```python
import os
import shutil
from keras.preprocessing.image import ImageDataGenerator, array_to_img, img_to_array, load_img
import tensorflow as tf
import numpy as np

mode = ['train','test']
cate = ['cardboard','glass','metal','paper','plastic']
for m in mode:
    base_dir = './data/trash_kaggle_train/'+m
    for i in cate:
        img_dir = './data/trash_kaggle_train/'+i # ./data/trash_kaggle_train/cardboard
        new_img_dir = i+'dir'
        new_img_dir  = os.path.join(base_dir,i+'100')
        os.mkdir(new_img_dir)
        os.listdir(new_img_dir)
        
        if m == 'train':
            fnames = [i+'{}.jpg'.format(n) for n in range(1,201)]
        elif m == 'test':
            fnames = [i+'{}.jpg'.format(n) for n in range(201,301)]
        for fname in fnames:
            src = os.path.join(img_dir,fname)
            dst = os.path.join(new_img_dir ,fname)
            shutil.copyfile(src,dst)

            
train_data = ImageDataGenerator(rescale=1./255,
shear_range=0.2,
zoom_range=0.2,
horizontal_flip=True)

training_set = train_data.flow_from_directory('./data/trash_kaggle_train/train',target_size=(64,64),
batch_size=32,class_mode='categorical')

test_data = ImageDataGenerator(rescale=1./255)
test_set = test_data.flow_from_directory('./data/trash_kaggle_train/test',target_size=(64,64),
batch_size=32,class_mode='categorical')

cnn = tf.keras.models.Sequential()
cnn.add(tf.keras.layers.Conv2D(filters=32,kernel_size=3,activation='relu',input_shape=[64,64,3]))
cnn.add(tf.keras.layers.MaxPool2D(pool_size=2,strides=2))
cnn.add(tf.keras.layers.Conv2D(filters=32,kernel_size=3,activation='relu',))
cnn.add(tf.keras.layers.MaxPool2D(pool_size=2,strides=2))
cnn.add(tf.keras.layers.Flatten())
cnn.add(tf.keras.layers.Dense(units=128,activation='relu'))
cnn.add(tf.keras.layers.Dense(units=1,activation='softmax'))
cnn.compile(optimizer='adam',loss='categorical_crossentropy',metrics=['accuracy'])
cnn.fit(x=training_set, validation_data= test_set, epochs=25)



```

```python
from keras.preprocessing import image
test_image = image.load_img('./data/trash_kaggle_train/train/plastic100/plastic1.jpg',target_size=(64,64))
test_image = image.img_to_array(test_image)
test_image = np.expand_dims(test_image,axis=0)
result = cnn.predict(test_image)
training_set.class_indices
if result[0][0]==1:
    prediction = 'plastic'
else:
    prediction = 'wrong'

print(prediction)
```

