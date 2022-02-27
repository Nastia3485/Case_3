# Case_3
"""Case-study #3 Анализ текста
Разработчики:
Галинская И.Е. 30%
Мишнева Е.A.   30%
Чужинова А.К.  50%

"""

from textblob import TextBlob
text = input("Введите текст: ")

quontity_sent = text.count(".")
sentencens = text.split(".")
qnt_wrd = []
for sent in sentencens:
    Words = sent.split()
    qnt_wrd.append(len(Words))
quantity_words = text.count(" ")+1
ASL=sum(qnt_wrd)/quontity_sent

vowel = ["а", "е", "ё", "и", "о", "у", "э", "ю", "я", "ы", "a", "e", "i", "o", "u", "y"]

qnt_vow = []
words = text.split()
for word in words:
    q=0
    word=word.lower()
    for x in word:
        if x in vowel:
            q+=1
    qnt_vow.append(q)
quantity_syll = sum(qnt_vow)
ASW=sum(qnt_vow)/quantity_words


text_blob_object = TextBlob(text)
blob = TextBlob(text)
try:
    text1 = str(blob.translate(to='en'))
except:
    text1=text
if text != text1:
    print("Перевод текста на английский при помощи TextBlob: ",text1)
    print("\n")
    FRE = 206.835 - (1.3 * ASL) - (60.1 * ASW)
else:
    FRE = 206.835 - (1.015 * ASL) - (84.6 * ASW)
analysisSub = TextBlob(text1).subjectivity
analysisPol = TextBlob(text1).polarity


print("Количество предложений: ",quontity_sent)
print("Средняя длина предложения в словах: ",ASL)
print("Количество слов: ",quantity_words)
print("Количество слогов: ",quantity_syll)
print("Средняя длина слова в слогах: ",ASW)
print("Индекс удобочитаемости Флеша: ", FRE)
if FRE > 80:
    print('Текст очень легко читается(для младших школьников).')
elif 80 <= FRE < 50:
    print('Простой текст (для школьников).')
elif 50 <= FRE < 25:
    print('Текст немного трудно читать (для студентов).')
else:
    print('Текст трудно читается (для выпускников ВУЗов).')
print("Объективность (в соответствии с переводом от TextBlob в случае ввода текста не на английском языке) : ",1-analysisSub)
print("Тональность: ",analysisPol)
if analysisPol < 0.5:
    print("Текст негативный")
elif analysisPol == 0.5:
    print("Текст нейтральный")
else:
    print("Текст позитивный")

