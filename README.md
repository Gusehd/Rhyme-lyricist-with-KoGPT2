# Rhyme-lyricist-with-KoGPT2

> KoGPT2 기반의 라임을 고려한 한국어 가사 생성 모델

GPT-2는 주어진 텍스트의 다음 단어를 잘 예측할 수 있도록 학습된 언어모델이며 문장 생성에 최적화 되어 있습니다.<br>
Rhyme-lyricist는 한국어 성능을 끌어올린 KoGPT2를 통해 구현한 라임을 고려한 가사 생성 모델 입니다.  
Colab 환경과 google drive를 통해 개발되었습니다.

## 구조 
<img width="100%" src="https://user-images.githubusercontent.com/79627126/170819770-3a53c1d5-340e-40d1-aad0-20ef257605af.png"/>

## 가사 생성 방법
1. 주어진 가사 데이터들로 KoGPT2 Fine Tuning 진행 ( 이미 Fine Tuning된 모델 사용시 스킵 )
2. 주어진 가사 데이터를 토큰화 ( 영단어의 경우 , 발음과 의미 포함 )
3. 토큰화된 단어들 중 Keyword와의 Rhyme score를 계산하여 나열 ( 영단어의 경우 발음을 통해서 진행 )
4. 일정 범위 내의 Rhyme score를 갖는 단어들을 word2vec으로 keyword와 얼마나 유사한지 검사 후 나열
5. Rhyme과 의미를 모두 고려하여 가사 생성에 사용될 단어들의 list가 생성됨
6. 해당 단어들을 통해 모델에 input으로 사용 , 라임을 고려한 가사 생성


## 다운로드
* Clone repository  
`git clone https://github.com/Capstonedesign0/AI-Composer.git`

* Colab  
`cd /gdrive/My Drive/Colab Notebooks`

* Requirements  
`!pip install -r requirements.txt`

* ETC  
 ++데이터 경로 재설정 필요
 
* Pre-fine tuning model download ( 90 ~ 19 년도 발라드 , 댄스 약 3500곡 학습 )   
   <a href = "https://drive.google.com/file/d/1D-XkGhv9qDhP2FHK22_qSJmkR3iVr38C/view?usp=sharing">구글 드라이브 다운로드</a>  
   ++ 경로 : corpus_data 폴더 안
   
* kor word2vec download    
   <a href = "https://drive.google.com/file/d/0B0ZXk88koS2KbDhXdWg1Q2RydlU/view?resourcekey=0-Dq9yyzwZxAqT3J02qvnFwg">구글 드라이브 다운로드</a>  
   <a href = "https://github.com/Kyubyong/wordvectors">박규병님의 깃허브</a>  
   ++ 경로 : 압축해제 후 나온 ko 폴더를 corpus_data 폴더안에 배치 
   
## 이용방법

* 모든 쉘 실행 후 마지막 쉘에서 다음 4가지 함수를 통해 가사 생성

* 함수 설명

1. `make_line(rhyme_word,word_len)` 
      * rhyme_word : 키워드 혹은 가사 생성시 사용할 미끼가사  
      * word_len : 전체 가사의 길이    
      * output : 라임을 고려하지 않은 일반적인 가사

2. `make_verse_seq(key_word,verse_maxlen, max_rhyme_hit,min_rhyme_hit,min_level=0)`

    * key_word : 가사에 처음으로 사용할 단어  
    * verse_maxlen : 전체 가사의 길이  
    * max_rhyme_hit : 사용할 단어들의 최대 라임 HIT  
    * min_rhyme_hit : 사용할 단어들의 최소 라임 HIT  
    * min_level=0 : 사용할 단어들의 word2vec 최소 유사도 ( 미만이면 사용 X )      
    * output : 라임을 고려한 일반적인 가사  

    시퀀스로 가사를 생성하는 방식 & 한단어로 가사를 만들고 그 위에 덮어 씌우는 방식

3. `make_verse_not_seq(key_word,verse_maxlen,one_verse_len, max_rhyme_hit,min_rhyme_hit,min_level=0)`
   * key_word : 가사에 처음으로 사용할 단어
   * verse_maxlen : 전체 가사의 줄의 개수
   * one_verse_len : 허용할 가사 한줄의 최대 길이
   * max_rhyme_hit : 사용할 단어들의 최대 라임 HIT
   * min_rhyme_hit : 사용할 단어들의 최소 라임 HIT
   * min_level=0 : 사용할 단어들의 word2vec 최소 유사도 ( 미만이면 사용 X )    

    여러 단어들을 통해 가사를 각각 한 줄씩 만들고 이후 합치는 방법으로 진행

4. `make_verse_chose_without_word2vec(
    key_word,verse_maxlen,one_verse_max_len,
    max_rhyme_hit,min_rhyme_hit,min_level=0)`

   * key_word : 가사에 처음으로 사용할 단어
   * verse_maxlen : 전체 가사의 줄의 개수
   * one_verse_len : 허용할 가사 한줄의 최대 길이
   * max_rhyme_hit : 사용할 단어들의 최대 라임 HIT
   * min_rhyme_hit : 사용할 단어들의 최소 라임 HIT
   * min_level=0 : 사용할 단어들의 word2vec 최소 유사도 ( 미만이면 사용 X )

   가사 생성은 모델이 진행하지만 , 선택은 사람이 할 수 있음  
   인공지능이 생성한 여러가지 가사들 중 사용자가 원하는 가사를 선택  
   한줄 한줄 이어나가 최종적인 가사 전체를 구성  

## 예시


## 목표

* Rhyme Score / Model 코드 분리
* Code Refactoring 진행
* Fine Tuning 데이터 확보 및 모델 재학습 ( 학습 데이터의 양이 너무 적음 )
* 힙합 ( 라임이 포함된 ) 가사로 모델 재학습 ( 댄스 , 발라드의 경우 라임 존재 X )
* 라임을 고려한 가사를 먼저 생성 후 , tuning 시키는 방식을 시도


## 한계

* 가사와 가사 사이의 연관성이 없음
* 모델 fine tunung에 사용된 데이터가 적음
* 의미있는 라임 가사를 생성하기 어려움


## Reference & Open-source library

hgtk : https://github.com/bluedisk/hangul-toolkit  
googletrans : https://github.com/ssut/py-googletrans  
request : https://github.com/psf/requests  
openpyxl : https://openpyxl.readthedocs.io/en/stable/  
pandas : https://pandas.pydata.org/   
발음변환 : "https://transliterator.herokuapp.com/"  
kor word2vec : https://github.com/Kyubyong/wordvectors  
pytorch : https://pytorch.kr/  
koGPT2 : https://github.com/SKT-AI/KoGPT2  
fastai : https://github.com/fastai/fastai  
transformers : https://github.com/huggingface/transformers  
kss : https://github.com/hyunwoongko/kss  


## Fine Tuning 진행시

* 주의 : 코드 구성은 xlsx 파일안의 lyrics 라는 열만을 가사로 인식함
* 새로 fine_tuning 하고자 한다면 데이터 전처리 필수
