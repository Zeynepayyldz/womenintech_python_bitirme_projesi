# Women in Tech Python Bitirme Projesi
**Merhabalar ben Zeynep, Sisterslab’in Toplum Gönüllüleri Vakfı (https://www.tog.org.tr/en/) tarafından desteklenen Woman in Tech Academy Projesi, Üniversite 3. & 4. sınıf öğrencisi veya üniversite mezunu, temel programlama bilgisine sahip, yazılım sektöründe çalışmak isteyen, 20-28 yaş arası 25 kadını 3 ay boyunca yazılım eğitimleriyle güçlendirerek sektörde iş gücüne katılımını hedefliyor. Ben de Woman in Tech Academy proje katılımcılarından biriyim. Teknoloji sektörü, cinsiyetçi rollerin dünya genelinde en ağır bastığı alanlardan biridir ve bu durumdan özellikle istihdama erişimde en çok etkilenen kitle ise kadınlardır. Bu problemden yola çıkarak geliştirilen Women in Tech Academy projesi hayata geçirilmiştir. Projeyle ilgili daha fazla bilgi almak için https://sisterslab.co/women-in-tech-academy/ linkine tıklayabilirsiniz.**

Bitirme Projem kapsamında, Covid-19 salgını ile ilgili bilgiler içeren csv dosyasını analiz ettim.

# Veri Setiyle İlgili Açıklamalar

Veri seti içerisinde; covid-19 salgını ile ilgili, günlük vaka sayısı, günlük ölüm sayısı, günlük aşılama, günlük test sayısı gibi bilgiler bulunmaktadır.

**Yapılacak Analizler ise şu şekildedir;**

1. Ülkelere göre günlük vaka sayısı.
2. Ülkelere göre ortalama vaka sayısı.
3. Ülkelere göre toplam aşılama sayısı.
4. Günlük ortalama vaka sayısı.
5. 

**Analizde Kullanılacak kütüphaneler şu şekildedir;**
* Pandas
* Numpy
* Seaborn
* Plotly
* Matplotlib

# Yapılan Analizlerin Sonuçları

Yapılan analiz sonuçlarından bazıları aşağıda verilmiştir. Analizlerle ilgili daha fazla ayrıntılara .ipynb uzantılı kod dosyasından erişebilirsiniz.

**Ülkelere göre günlük vaka sayısının bulunması;**


```
import plotly.express as px
daily_case=covid.dropna(subset=['new_cases'])
fig = px.line(daily_case, x="date", y="new_cases", color='location')  # ülkelere göre günlük vaka sayısı 
fig.update_layout({'yaxis_title':'Number of Daily Cases by Country. ','xaxis_title':'Date'})
fig.show()
```

**Ülkelere göre ortalama vaka sayısının bulunması;**


```
import plotly.express as px

df2=covid.dropna(subset=['new_cases'])
average_case=df2.groupby('location')['new_cases'].mean()
fig = px.bar(average_case, y='new_cases')
fig.update_layout({'yaxis_title':'Average Number of Cases by Country ','xaxis_title':'Location'})
fig.show()
```

**Ülkelere göre toplam aşılama sayısının bulunması;**


```
df3=covid.dropna(subset=['total_vaccinations'])
total_vac=df3.groupby('location')['total_vaccinations'].max()

fig = px.bar(total_vac,y='total_vaccinations')
fig.update_layout({'yaxis_title':'Total Number of Vaccinations by Country','xaxis_title':'Location'})
fig.show()

```

**Günlük ortalama vaka sayısının bulunması;**


```
df4=covid.dropna(subset=['new_cases'])
daily_average_case = df4.groupby('date')['new_cases'].mean()

fig = px.bar(daily_average_case, y='new_cases')
fig.update_layout({'yaxis_title':'Average number of cases per day','xaxis_title':'Date'})
fig.show()

```

**EK OLARAK YAPILAN ANALİZLER**

**Ülkelere göre günlük ölüm sayısının analizi;** 

```

import plotly.express as px
death_case=covid.dropna(subset=['new_cases'])
fig = px.line(death_case, x="date", y="new_deaths", color='location')
fig.update_layout({'yaxis_title':'Number of Daily Deaths by Country','xaxis_title':'Date'})
fig.show()

```

**Aşılamanın ölüm üzerindeki etkisinin analizi;**

```
death_vaccinations=covid.groupby('location')["total_deaths", "total_vaccinations",'total_cases','gdp_per_capita'].max()
death_vaccinations.dropna(inplace=True)
death_vaccinations.reset_index(inplace=True)
death_vaccinations

```
![UU](https://octodex.github.com/images/yaktocat.png)

