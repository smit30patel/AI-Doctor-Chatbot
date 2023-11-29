
# AI-Doctor-chatbot

The AI Doctor Chatbot is an artificial intelligence-powered virtual assistant designed to provide users with medical information, answer health-related queries, and offer guidance on various health concerns. It aims to enhance access to healthcare information and promote well-being.

## Run command 

```bash
  flutter packages get
  flutter run   
```

# Demo

 ![alt text](https://i.imgur.com/KcI2plh.png) 

# Tools Used

App Building - Flutter \
User Account - Firebase \
User Interface - List View widget and custom TaskWidget Photo of app here ![alt text](https://i.stack.imgur.com/oKe8d.png) \
Payments - Razorpay(India), Stripe(elsewhere in the world) ![alt text](https://marketplace.appthemes.com/files/2017/05/app-razorpay-title-screenshot.png) \
Voice Recognition plugin - (custom channel, ios Speech API, Android SpeechRecognizer) ![alt text](https://i.stack.imgur.com/qAFtd.png) \
Deep Learning Model - BioBERT , input question into retrained bioBERT to convert into an embedding. Input the embedding into a fully connected neural network, output an embedding for similarity lookup. Most similar Q&A's used by GPT-2 to generate an answer. ![alt text](https://cdn-images-1.medium.com/max/1600/1*q2OjkfFaUb8L_g6K6PGlWQ.png) 


# App Design 

## 1.Building Flutter app

![alt text](https://www.cleveroad.com/images/article-previews/advantages-flutter.png)  


- Step 1 - Download Base code https://github.com/rxlabz/sytody 
- Step 2 -  Install and run base code 
- Step 3 - Analyze Base Code 
- Main -  Runs the top level widget (the app itself) in one line of code 
- Styody_app - Defines a navigation bar and a listview \
- Transcriptor - Implements Recognizor, transcription, and task creation in the listview 
- Recognizer - This is the interface that defines how the voice interaction functionality is communicated between Flutter's Dart Code and the native voice modules for each mobile platform (Java and Obj-C) 
- Task - Defines what each widget inside the list contains (text, color, alignments) 
- Languages - for different language string constants 

## Add Login/Signup

- Lol this guy made this same guy speech recognition plugin, props  https://pub.dev/packages/speech_recognition

- We must open a channel to speak from Dart to the host platform (iOS or Android)
- 2 Methods are available (MethodChannel Dart <> host function passing, and BasicMessageChannel (Dart <> Host data passing))
- The channels allow for the passing of basic data between Dart <> Host (strings, maps, lists, numbers, etc.)

To create a plugin available publically for anyone we do 3 steps \
 
    1. "flutter create  --org my.domain  --plugin plugin_name" 
    2. Write code for the generated Dart, Java, and ObjC platforms 
    3. Run "flutter pub publish"

## BERT Explained

First of all, when Google released BERT, it was like the ImageNet moment in computer vision, but this time for natural langugage processing. It was a big deal. Now everyone can use the weights file that bert learned after training on millions of words as a starting point for their specific NLP task, be it Q&A, sentence classfiication, sentence generation, sentiment analysis, etc. 

![alt text](https://cdn-images-1.medium.com/max/1600/0*bXDn2DeiusVVIv6S )

-  “I accessed the bank account,”  BERT is bidirectional, takes into context 'i accesed' and 'account' when classifying the word bank
- trained on unsupervised wikipedia data. lots of it. it built useful word representations. Knowledge. It's automated knowledge. 

I have a video on how it works, see this , now i'll rap

https://www.youtube.com/watch?v=bDxFvr1gpSU

## BioBERT Explained

https://github.com/dmis-lab/biobert Good Job Korea University. 


- Published 5 months ago
- It's a pre-trained biomedical language representation model. The full name is "BiDirection Encoder Reprenseatitions froM Transformers for Biomedical Text Mining". 
-BioBERT outperforms plain old BERT on 3 tasks; Biomedical Named Entity Recognition, Biomedical Relation Extraction, and Biomedical Question Answering
- The pretrained weights are freely available here https://github.com/naver/biobert-pretrained 
- It was trained on 200K questions from PubMed, 270K from PubMed central, 
![alt text](https://cdn-images-1.medium.com/max/1200/1*AP4lIEW-THPNJwj4gLKTlA.png)

## DOT Product Explained

- Then I found this clever model pretrained with BioBERT. Which itself was pretrained on BERT. That's meta AF https://github.com/re-search/DocProduct 
- Dot Product can perfrom Q&A on biomedical data, a digital doctor! 

![alt text](https://camo.githubusercontent.com/b9ce3382ce50b3cf59ffc061aa9b268bfe27182d/68747470733a2f2f692e696d6775722e636f6d2f777a57743033392e706e67)



## Integrating pretrained model into our flutter app

It's saved as an H5 file in keras. We can use the TFLiteConverter to turn it into a tflite file 


```python 
from tensorflow.contrib import lite
converter = lite.TFLiteConverter.from_keras_model_file( 'model.h5')
tfmodel = converter.convert()
open ("model.tflite" , "wb") .write(tfmodel)
```





