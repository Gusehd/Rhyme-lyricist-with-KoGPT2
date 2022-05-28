# Rhyme-lyricist-with-KoGPT2

> KoGPT2 기반의 라임을 고려한 한국어 가사 생성 모델

GPT-2는 주어진 텍스트의 다음 단어를 잘 예측할 수 있도록 학습된 언어모델이며 문장 생성에 최적화 되어 있습니다.<br>
Rhyme-lyricist는 한국어 성능을 끌어올린 KoGPT2를 통해 구현한 라임을 고려한 가사 생성 모델 입니다.

## 구조 
<img width="100%" src="https://user-images.githubusercontent.com/79627126/170819770-3a53c1d5-340e-40d1-aad0-20ef257605af.png"/>

## 가사 생성 방법
1. 주어진 가사 데이터들로 KoGPT2 Fine Tuning 진행 ( 이미 Fine Tuning된 모델 사용시 스킵 )
2. 주어진 가사 데이터를 토큰화 ( 영단어의 경우 , 발음과 의미 포함 )
3. 토큰화된 단어들 중 Keyword와의 Rhyme score를 계산하여 나열 ( 영단어의 경우 발음을 통해서 진행 )
4. 일정 범위 내의 Rhyme score를 갖는 단어들을 word2vec으로 keyword와 얼마나 유사한지 검사 후 나열
5. Rhyme과 의미를 모두 고려하여 가사 생성에 사용될 단어들의 list가 생성됨
6. 해당 단어들을 통해 모델에 input으로 사용 , 라임을 고려한 가사 생성


## 이용방법
* Clone repository  
`git clone https://github.com/Capstonedesign0/AI-Composer.git`

* Colab  
`cd /gdrive/My Drive/Colab Notebooks`

* ETC  
 ++데이터 경로 재설정 필요

* Pre-fine tuning model download  
 <a href = "https://drive.google.com/file/d/1D-XkGhv9qDhP2FHK22_qSJmkR3iVr38C/view?usp=sharing">구글 드라이브 다운로드</a>


## 목표

* Rhyme Score / Model 코드 분리
* Code Refactoring 진행
* Fine Tuning 데이터 확보 및 모델 재학습 ( 데이터의 양이 너무 적음 )
* 


## 한계


## Reference & Open-source library

hgtk : https://github.com/bluedisk/hangul-toolkit
googletrans : https://github.com/ssut/py-googletrans
request : https://github.com/psf/requests
openpyxl : https://openpyxl.readthedocs.io/en/stable/
pandas : https://pandas.pydata.org/
"https://transliterator.herokuapp.com/"
https://github.com/Kyubyong/wordvectors
https://pytorch.kr/
koGPT2 : https://github.com/SKT-AI/KoGPT2
fastai : https://github.com/fastai/fastai
transformers : https://github.com/huggingface/transformers
kss : https://github.com/hyunwoongko/kss


## 정리해야할 것

#주의 : 코드 구성은 xlsx 파일안의 lyrics 라는 열만을 가사로 인식함
#새로 fine_tuning 하고자 한다면 데이터 전처리 필수
