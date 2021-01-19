# speech_project_press_release

DESCRIPTION:

In this repository, you will find the analyzes of the press release of some political parties in Germany
Also, you will find models to predict Which press release belongs to which political party


DATA:

CDU's press release: https://www.cdu.de/presse/pressemitteilungen

SPD's press release: https://www.spd.de/presse/pressemitteilungen/

Grünen's press release: https://www.gruene-bundestag.de/presse/pressemitteilungen

Die Linke's press release: https://www.linksfraktion.de/presse/pressemitteilungen/


examples of some important used methods:


#after having all elements by giving xpath, getting text values for each element

	text = WebDriverWait(driver, 30).until(
        EC.presence_of_all_elements_located((By.XPATH, '//*[@id="c5882"]/div/div[3]/div/div/article/a/div/div[2]' ))
        )

    grn_text = []
	for i in text:
    	grn_text.append(i.text) 


#to drop certain elements

	df = df[df['label']!='Die Linke']


#to eliminating some words, which might mislead our model 

	def common(data):
	    data = data.split()
	    ret = []
	    for i in data:
	        if i.lower() not in ['cdu','pressemitteilung' ,'pressestelle', 'spd','pressekonferenz','linke','grünen', 'erklärt']:
	              ret.append(i)
	    return " ".join(ret)

#an easy way to drop a given value by using index

	df_s.drop(list(df_s[df_s.sentece==""].index), inplace=True)

Some insights:

1) In order to access data I used Selenium

2) There are some unbalances among political parties, the storage type can be a reason.  

3) For each speech there are some sentences as salutations. That's why I preferred to drop them. Moreover, 'pressemitteilung', etc, are used too much by the political parties. But in my opinion, these words should be dropped as well since it does not give insight deeply.
 

4) After dropping some intro sentences and some repeated words, the distribution of words changed, and it may give some important insights.

6) As a result;
    6.1) The prediction for the whole press release is really impressive, but it is reduced for sentences. 
    6.2) For the whole press release the logistic regression worked very well, it predicted without any failure
    6.3) For the sentence level, several models  are applied, but overfitting and performance were major problems
    6.4) So that, the logistic regression predicted also better than other models for sentence prediction. as well.
7) In terms of analyzing features of releases, firstly it may not be optimized available truly because of automation problems. Therefore the balance amongst the releases from the parties was an important issue. On the other hand, regarding the number of releases in the dataset, it was well balanced, whereas the timeline for each party differentiates a lot from one to another. Interestingly the size of the release also was quite changeable among the parties. 

Limitation & Further:
1) With not only more but also balanced data, and deployment of different models better results can be obtained for sentence prediction. 
2) Dropping more unnecessary and repeated words might also provide better results






