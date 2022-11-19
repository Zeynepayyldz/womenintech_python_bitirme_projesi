# Women in Tech Python Bitirme Projesi
**Merhabalar ben Zeynep, Sisterslab’in Toplum Gönüllüleri Vakfı (https://www.tog.org.tr/en/) tarafından desteklenen Woman in Tech Academy Projesi, Üniversite 3. & 4. sınıf öğrencisi veya üniversite mezunu, temel programlama bilgisine sahip, yazılım sektöründe çalışmak isteyen, 20-28 yaş arası 25 kadını 3 ay boyunca yazılım eğitimleriyle güçlendirerek sektörde iş gücüne katılımını hedefliyor. Ben de Woman in Tech Academy proje katılımcılarından biriyim. Teknoloji sektörü, cinsiyetçi rollerin dünya genelinde en ağır bastığı alanlardan biridir ve bu durumdan özellikle istihdama erişimde en çok etkilenen kitle ise kadınlardır. Bu problemden yola çıkarak geliştirilen Women in Tech Academy projesi hayata geçirilmiştir. Projeyle ilgili daha fazla bilgi almak için https://sisterslab.co/women-in-tech-academy/ linkine tıklayabilirsiniz.**

Bitirme Projem kapsamında, Covid-19 salgını ile ilgili bilgiler içeren csv dosyasını analiz ettim.

![0](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/bb3cd67cd6c8f8faa8882d2e2725c649.gif?raw=true)

[This is an external link to genome.gov](https://www.genome.gov/)


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
* Seaborn
* Plotly
* Matplotlib

# Yapılan Analizlerin Sonuçları

Yapılan analiz sonuçlarından bazıları aşağıda verilmiştir. Analizlerle ilgili daha fazla ayrıntılara .ipynb uzantılı kod dosyasından erişebilirsiniz.

**Covid-19 veri setinde eksik verilerin raporlanması;**

```
import plotly.express as px
import pandas as pd
covid_nulls=pd.DataFrame(covid[['total_cases','total_deaths','total_vaccinations','new_cases','new_vaccinations']].isnull().sum(),columns=['r'])
covid_nulls=covid_nulls.reset_index()
fig = px.line_polar(covid_nulls, r='r', theta='index', line_close=True)
fig.show("png")

```
![1](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/1-eksik_veri.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/eksik_veri.html

**Ülkelere göre günlük vaka sayısının bulunması;**

```
import plotly.express as px
daily_case=covid.dropna(subset=['new_cases'])
fig = px.line(daily_case, x="date", y="new_cases", color='location')  # ülkelere göre günlük vaka sayısı 
fig.update_layout({'yaxis_title':'Number of Daily Cases by Country. ','xaxis_title':'Date'})
fig.show()
```
![2](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/2-ulkelere_gore_gunluk_vaka.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/ulkelere_gore_gunluk_vaka.html

**Ülkelere göre ortalama vaka sayısının bulunması;**


```
import plotly.express as px

df2=covid.dropna(subset=['new_cases'])
average_case=df2.groupby('location')['new_cases'].mean()
fig = px.bar(average_case, y='new_cases')
fig.update_layout({'yaxis_title':'Average Number of Cases by Country ','xaxis_title':'Location'})
fig.show()
```
![3](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/3-ulkelere_gore_ortalama_vaka.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/ulkelere_gore_ortalama_vaka.html

**Ülkelere göre toplam aşılama sayısının bulunması;**


```
df3=covid.dropna(subset=['total_vaccinations'])
total_vac=df3.groupby('location')['total_vaccinations'].max()

fig = px.bar(total_vac,y='total_vaccinations')
fig.update_layout({'yaxis_title':'Total Number of Vaccinations by Country','xaxis_title':'Location'})
fig.show()

```
**Ülkelere göre sıralanmış ortalama vaka sayısının bulunması;**
```
plt.figure(figsize=(50,10))
plt.ylabel('Average Number of Cases by Country')
covid.groupby("location")["new_cases"].mean().sort_values(ascending=False).plot.bar(width= 5, fontsize=15, color="#87CEEB") 

```

![4](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/4-siralanmis_ulkelere_gore_ortalama_vaka.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/siralanmis_ulkelere_gore_ortalama_vaka.html

**Ülkelere göre toplam aşılama sayısının bulunması;**

```
df3=covid.dropna(subset=['total_vaccinations'])
total_vac=df3.groupby('location')['total_vaccinations'].max()

fig = px.bar(total_vac,y='total_vaccinations')
fig.update_layout({'yaxis_title':'Total Number of Vaccinations by Country','xaxis_title':'Location'})
fig.show("png")

```
![5](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/5-ulkelere_gore_toplam_asilama.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/ulkelere_gore_toplam_asilama.html


**Günlük ortalama vaka sayısının bulunması;**


```
df4=covid.dropna(subset=['new_cases'])
daily_average_case = df4.groupby('date')['new_cases'].mean()

fig = px.bar(daily_average_case, y='new_cases')
fig.update_layout({'yaxis_title':'Average number of cases per day','xaxis_title':'Date'})
fig.show("png")

```
![6](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/6-dunya_gunluk_ortalama_vaka.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/dunya_gunluk_ortalama_vaka.html

**EK OLARAK YAPILAN ANALİZLER**

**Ülkelere göre günlük ölüm sayısının analizi;** 


```

import plotly.express as px
death_case=covid.dropna(subset=['new_cases'])
fig = px.line(death_case, x="date", y="new_deaths", color='location')
fig.update_layout({'yaxis_title':'Number of Daily Deaths by Country','xaxis_title':'Date'})
fig.show("png")

```
![7](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/7-ulkelere_gore_gunluk_olum.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/ulkelere_gore_gunluk_olum.html

**Aşılamanın ölüm üzerindeki etkisinin analizi;**

```
death_vaccinations=covid.groupby('location')["total_deaths", "total_vaccinations",'total_cases','gdp_per_capita','population'].max()
death_vaccinations.dropna(inplace=True)
death_vaccinations.reset_index(inplace=True)
death_vaccinations

death_vaccinations['death_ratio'] = death_vaccinations['total_deaths'] / death_vaccinations['total_cases']
death_vaccinations['vac_ratio'] = death_vaccinations['total_vaccinations'] / death_vaccinations['population']
death_vaccinations['case_ratio'] = death_vaccinations['total_cases'] / death_vaccinations['population']
fig = px.scatter(death_vaccinations, x="case_ratio", y="vac_ratio",size="death_ratio",color='location',log_x=1)
fig.show("png")

```
![8](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/8-ulkelere_gore_asilama_vaka_olum_orani.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/ulkelere_gore_asilama_vaka_olum_orani.html

**Sigara içen kadınlarda toplam ölüm analizi;**

```
smoker_death=covid.groupby('location')[['female_smokers', 'male_smokers', 'total_deaths', 'total_cases','gdp_per_capita','total_vaccinations','population']].max()
smoker_death.dropna(inplace=True)
smoker_death.reset_index(inplace=True)

```
```
fig = px.scatter(smoker_death, x="total_deaths", y="female_smokers", trendline="lowess", color='location', log_x=1)
fig.show("png")

```
![9](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/9-kadin_sigara_toplam_olum.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/kadin_sigara_toplam_olum.html


**Sigara içen erkeklerde toplam ölüm analizi;**

```
fig = px.scatter(smoker_death, x="total_deaths", y="male_smokers", trendline="lowess", color='location', log_x=1)
fig.show("png")
```
![10](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/10-erkek_sigara_toplam_olum.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/erkek_sigara_toplam_olum.html

**Sigara içen kadın ver erkeklerde ölüm oranının analizi**

smoker_death['death_ratio'] = smoker_death['total_deaths'] / smoker_death['total_cases']

```
fig = px.scatter(smoker_death, x="male_smokers", y="female_smokers", trendline="lowess", color='location', size='death_ratio', log_x=1)
fig.show("png")
```
![11](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/11-kadin_erkek_sigara_olum_orani.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/kadin_erkek_sigara_olum_orani.html

**Kişi başı gelir düzeyine -GDP per Capita- bağlı ölüm oranı analizi;**

```
smoker_death.sort_values(by='gdp_per_capita',inplace=True)
smoker_death['death_ratio'] = smoker_death['total_deaths'] / smoker_death['total_cases']
fig = px.line(smoker_death,x='gdp_per_capita',y='death_ratio',hover_name='location')
fig.add_vrect(
    x0=0, x1=15000,
    annotation_text="low", annotation_position="top",
    fillcolor="skyblue", opacity=0.5,
    layer="below", line_width=0,
),
fig.add_vrect(
    x0=15000, x1=30000,
    annotation_text="middle", annotation_position="top",
    fillcolor="Salmon", opacity=0.5,
    layer="below", line_width=0,
),
fig.add_vrect(
    x0=30000, x1=60000,
    annotation_text="middle-high", annotation_position="top",
    fillcolor="lightgray", opacity=0.5,
    layer="above", line_width=0,
),
fig.add_vrect(
    x0=60000, x1=120000,
    annotation_text="high", annotation_position="top",
    fillcolor="gray", opacity=0.5,
    layer="below", line_width=0,
),

fig.update_layout(title='<b>Kişi Başı Gelir Düzeyine Bağlı Olarak Ölüm Oranı<b>',
                  xaxis_title='Gdp per Capita', 
                  yaxis_title='Death Ratio',
                  titlefont={'size': 24},
                  font_family = 'San Serif',
                  width=950,height=500,
                  template="simple_white",
                  showlegend=True,
                  paper_bgcolor="white",
                  font=dict(
                      color ='black',
                      ),
                  legend=dict(
                      orientation="v",
                      y=1, 
                      yanchor="bottom", 
                      x=1.0, 
                      xanchor="right",)   
 )
fig.show("png")
```

![12](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/12-gdp_death_ratio.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/gdp_death_ratio.html

**Kişi başı gelir düzeyine -GDP per Capita- bağlı olarak aşılama oranı analizi;**

```
smoker_death.sort_values(by='gdp_per_capita',inplace=True)
smoker_death['vac_ratio'] = smoker_death['total_vaccinations'] / smoker_death['population']
fig = px.line(smoker_death,x='gdp_per_capita',y='vac_ratio',hover_name='location')
fig.add_vrect(
    x0=0, x1=15000,
    annotation_text="low", annotation_position="top",
    fillcolor="skyblue", opacity=0.5,
    layer="below", line_width=0,
),
fig.add_vrect(
    x0=15000, x1=30000,
    annotation_text="middle", annotation_position="top",
    fillcolor="Salmon", opacity=0.5,
    layer="below", line_width=0,
),
fig.add_vrect(
    x0=30000, x1=60000,
    annotation_text="middle-high", annotation_position="top",
    fillcolor="lightgray", opacity=0.5,
    layer="above", line_width=0,
),
fig.add_vrect(
    x0=60000, x1=120000,
    annotation_text="high", annotation_position="top",
    fillcolor="gray", opacity=0.5,
    layer="below", line_width=0,
),

fig.update_layout(title='<b>Kişi Başı Gelir Düzeyine Bağlı Olarak Nüfusun Aşılanma Oranı<b>',
                  xaxis_title='Gdp per Capita', 
                  yaxis_title='Vaccination Ratio',
                  titlefont={'size': 24},
                  font_family = 'San Serif',
                  width=950,height=500,
                  template="simple_white",
                  showlegend=True,
                  paper_bgcolor="white",
                  font=dict(
                      color ='black',
                      ),
                  legend=dict(
                      orientation="v",
                      y=1, 
                      yanchor="bottom", 
                      x=1.0, 
                      xanchor="right",)   
 )
fig.show("png")
```
![13](https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/images/13-gdp_vac_ratio.png)
[See the HTML!](https://htmlpreview.github.io/?https://github.com/Zeynepayyldz/womenintech_python_bitirme_projesi/blob/main/htmls/gdp_vac_ratio.html





![UU](https://octodex.github.com/images/yaktocat.png)

