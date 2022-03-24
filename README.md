

#  Estimating Refugee Impact 

---

Using UN and World Bank data, can we estimate the financial impact to host countries of Ukrainian refugees in a way that be replicated in lower and middle income countries?

### Authors: 

Jason Meyers, Tim O'Neill, Ben Roberts, Tori Powers


## Table of Contents
1. Executive Summary
2. Context
3. Sources & Data Dictionary
4. Analysis
5. Conclusions
6. Recommendations

## Executive Summary
---
As of late March 2022 Russia's invasion of Ukraine has displaced approximately [10 million](https://www.globalprotectioncluster.org/wp-content/uploads/Update-on-IDP-Figures-in-Ukraine-18-March.pdf) Ukrainians, roughly a quarter of the country's total reported population. Approximately three and a half million Ukrainians have fled to neighboring countries. Foreign governments and international organizations are rushing to help meet the humanitarian needs of the Ukrainians fleeing violence, raising questions about the economic impact to neighboring countries. Some research shows that human migration can be a net economic positive to the host countries, suggesting that providing humanitarian support may be in the interest of host nations. As a first step towards building a generalized model, this project uses World Bank and United Nations data to provide an initial exploration of how human refugee flows may impact the economies of host nations. 


### Definitions and Scope

This study focuses on the impact of  international refugee movements, relying on the UN definition of refugee as: 

> A person who, “owing to a well-founded fear of persecution for reasons of race, religion, nationality, membership of a particular social group or political opinions, is outside the country of his nationality and is unable or, owing to such fear, is unwilling to avail himself of the protection of that country.”)

Upon researching economic impact of refugees globally, it was noted that there is much information on the impact to high income countries, less information available on the impact to low and middle income countries. This study seeks to build a model that can effectively estimate the impact of refugees in  Ukrainian refugee host countries with the hopes of in the future generalizging our model to similar impacts in low and middle income countries. 

## Context
---

The current influx of Ukrainian refugees represents a dramatic spike in refugee flow in Europe. From 2013-2021 approximately 6 million people sought asylum in the European Union, with 2.5 million entering in 2015 and 2016, many as a result of Russia's seizure of Crimean in 2014. (Source??)

### Refugee Border Crossings

![](https://cdn.vox-cdn.com/uploads/chorus_asset/file/23328541/Ukrainian_refugee_escape_routes.jpg)
([*source*](https://cdn.vox-cdn.com/uploads/chorus_asset/file/23328541/Ukrainian_refugee_escape_routes.jpg))

### Ukrainian Refugee Flows as of March 2022

| Receiving Nation     | Information Source  |     Data Date |     Total |
| :------------------- | :------------------ | ------------: | --------: |
| Poland               | National Government | 22 March 2022 | 2,083,854 |
| Romania              | National Government | 22 March 2022 |   535,461 |
| Republic of Moldova* | National Government | 22 March 2022 |   371,104 |
| Hungary              | National Government | 22 March 2022 |   312,120 |
| Russian Federation   | National Government | 22 March 2022 |   231,764 |
| Slovakia             | National Government | 22 March 2022 |   250,036 |
| Belarus              | National Government | 22 March 2022 |     3,735 |

*Lack of data prevented Moldova's inclusion in our study. 

Source: [Eurostat](https://www.vox.com/22983230/europe-ukraine-refugees-charts-map), via Vox.

#### Literature Review

The economic implications of voluntary and involuntary human migration are generally well understood for developed nations, but less so for poor or developing countries. A brief survey of the literature on refugee flows finds the following:

- For developed countries, refugees as well as economic migrants have limited impact on wages and unemployment, with some downward pressure on wages among low-skilled workers. Refugees have minimal if any fiscal impacts. (Borjas 2003, D'Amuri et al., 2010, OECD 2013).
- For low and middle income countries, there are winners and losers within the host nation economy, with certain population segments experiencing more significant economic challenges than others (Facchini et al., 2013, Ozden and Wagner 2014, Gindling 2009).
- The time frame, rate, and duration of the displacement will heavily shape the costs and contributions of refugees to the host country. First-order financial impacts, especially in aggregate demand, may outweigh tangible benefits in the short-term, while labor supply effects develop gradually over time (IMF). Sharp increases will likely impose greater challenges and costs in the near-term. (Kulhman, 1990, IMF 2017)
- The socioeconomic characteristics of the refugees themselves, macroeconomic factors in the host economy, and policy choices by host nations can shape the role refugees can play in the host economy. (Khoudour and Andersson, OECD 2017).



## Sources & Data Dictionary
---
Data from World Bank and UNHCR was gathered and narrowed down to the years of 2016-2020.  In the process of cleaning the data, multiple columns were removed due to vast amounts of missing dat. We decided on using GDP Annual Percentage Change as our target variable representing economic impact. We used thirty-one economic features for 148 countries spanning the years 2016 - 2019 in order to build a predictive model. 

#### Sources
This model relied on the following data sources:

| Source                                                | Data                                     | Reference                                                    | Description                               |
| ----------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------ | ----------------------------------------- |
| World Bank                                            | *World Development Indicators* Databank. | [Link](https://databank.worldbank.org/source/world-development-indicators) | We downloaded 40+ economic indicators for |
| United Nations High Commissioner for Refugees (UNHCR) | UNHCR Data/Global Public API             | [Link](https://www.unhcr.org/data.html)                      |                                           |

#### Data Dictionary

| Feature                                                      | Type    | Domain                       | Description                                                  |
| ------------------------------------------------------------ | ------- | ---------------------------- | ------------------------------------------------------------ |
| Year                                                         | year    | 2016-2019                    | The given year of reporting.                                 |
| Country                                                      | object  | name                         | Specific Country reporting data.                             |
| Refugees under UNHCR's mandate                               | int     | 0- 3,681,688                 | Persons who have fled their country because their lives, safety or freedom have been threatened by generalised violence, foreign aggression, internal conflicts, massive violation of human rights or other circumstances which have seriously disturbed public order. |
| Asylum-seekers                                               | int     | 0 - 847,608                  | Someone whose request for sanctuary has yet to be processed. Every year, around one million people seek asylum. National asylum systems are in place to determine who qualifies for international protection |
| IDPs of concern to UNHCR                                     | int     | 0 - 7,976,412                | Internally displaced persons (IDPs). Refugees have crossed international borders and are entitled to protection and assistance from the states into which they move and from the international community through the United Nations (UN) and its specialist agencies. IDPs, on the other hand, are displaced within their own countr. |
| Stateless persons                                            | int     | 0 - 955,399                  | A person who is not considered as a national by any State under the operation of its law”. In simple terms, this means that a stateless person does not have the nationality of any country. Some people are born stateless, but others become stateless. |
| Others of concern                                            | int     | 0 - 2,304,506                | A person of concern is any person whom the United Nations High Commissioner on Refugees (UNHCR), the UN Refugee Agency, considers a refugee, internally displaced person (IDP), asylum- seeker, or stateless person, with some additional persons not fitting these criteria. This number represents those not fitting these criteria. |
| Ref and Asyl                                                 | int     | 0 - 3,993,387                | A summation of Reguees under UNHCR's manadate and Asylum Seekers |
| SUM REFUGEE                                                  | int     | 5 - 8,386,151                | A summation of all persons of concer, Reguees under UNHCR's manadate, Asylum Seekers, IDPs of concern, and Others |
| GDP_annual_change                                            | percent | (-7.157247, 13.787373)       | Annual percentage growth rate of GDP at market prices based on constant local currency |
| Adjusted savings: net national savings (current \$USD)       | float   | -6.158226e+10 - 3.850000e+12 | Net national savings are equal to gross national savings less the value of consumption of fixed capital. |
| Adjusted savings: particulate emission damage (current US\$) | float   | 3.598443e+06 - 6.362669e+10  | Particulate emissions damage is the damage due to exposure of a country's population to ambient concentrations of particulates measuring less than 2.5 microns in diameter (PM2.5), ambient ozone pollution, and indoor concentrations of PM2.5 in households cooking with solid fuels. |
| Adolescent fertility rate (births per 1,000 women ages 15-19) | float   | 1.261800 - 189.379000        | Adolescent fertility rate is the number of births per 1,000 women ages 15-19. |
| Air transport, passengers carried                            | int     | 8.570000e+02 - 9.267370e+08  | Air passengers carried include both domestic and international aircraft passengers of air carriers registered in the country. |
| Current health expenditure (% of GDP)                        | float   | 2.229710 - 16.844324         | Level of current health expenditure expressed as a percentage of GDP. Estimates of current health expenditures include healthcare goods and services consumed during each year. This indicator does not include capital health expenditures such as buildings, machinery, IT and stocks of vaccines for emergency or outbreaks. |
| Current health expenditure per capita (current US\$)         | float   | 18.520622 - 10921.012700     | Current expenditures on health per capita in current US dollars. Estimates of current health expenditures include healthcare goods and services consumed during each year. |
| Death rate, crude (per 1,000 people)                         | float   | 1.169000 - 15.500000         | Crude death rate indicates the number of deaths occurring during the year, per 1,000 population estimated at midyear. Subtracting the crude death rate from the crude birth rate provides the rate of natural increase, which is equal to the rate of population change in the absence of migration. |
| Domestic general government health expenditure per capita (current US\$) | float   | 1.811401 - 7089.27213        | Public expenditure on health from domestic sources per capita expressed in current US dollars. |
| Domestic private health expenditure per capita (current US\$) | float   | 3.455277 - 6788.967168       | Current private expenditures on health per capita expressed in current US dollars. Domestic private sources include funds from households, corporations and non-profit organizations. Such expenditures can be either prepaid to voluntary health insurance or paid directly to healthcare providers. |
| Ease of doing business score (0 = lowest performance to 100 = best performance) | float   | 34.390280 - 87.166330        | The ease of doing business scores benchmark economies with respect to regulatory best practice, showing the proximity to the best regulatory performance on each Doing Business indicator. An economy’s score is indicated on a scale from 0 to 100, where 0 represents the worst regulatory performance and 100 the best regulatory performance. |
| Fixed broadband subscriptions (per 100 people)               | float   | 0.001229 - 46.820499         | Fixed broadband subscriptions refers to fixed subscriptions to high-speed access to the public Internet (a TCP/IP connection), at downstream speeds equal to, or greater than, 256 kbit/s. This includes cable modem, DSL, fiber-to-the-home/building, other fixed (wired)-broadband subscriptions, satellite broadband and terrestrial fixed wireless broadband. This total is measured irrespective of the method of payment. It excludes subscriptions that have access to data communications (including the Internet) via mobile-cellular networks. It should include fixed WiMAX and any other fixed wireless technologies. It includes both residential subscriptions and subscriptions for organizations. |
| Fixed telephone subscriptions (per 100 people)               | float   | 0 - 60.317690                | Fixed telephone subscriptions refers to the sum of active number of analogue fixed telephone lines, voice-over-IP (VoIP) subscriptions, fixed wireless local loop (WLL) subscriptions, ISDN voice-channel equivalents and fixed public payphones. |
| GNI growth (annual percent)                                  | float   | -13.091265 - 14.171282       | GNI (formerly GNP) is the sum of value added by all resident producers plus any product taxes (less subsidies) not included in the valuation of output plus net receipts of primary income (compensation of employees and property income) from abroad. |
| International tourism, expenditures (current US\$)           | float   | 2.100000e+06 - 1.860000e+11  | International tourism expenditures are expenditures of international outbound visitors in other countries, including payments to foreign carriers for international transport. These expenditures may include those by residents traveling abroad as same-day visitors, except in cases where these are important enough to justify separate classification. For some countries they do not include expenditures for passenger transport items. Data are in current U.S. dollars. |
| International tourism, receipts (current US\$)               | float   | 1.600000e+06 - 2.420000e+11  | International tourism receipts are expenditures by international inbound visitors, including payments to national carriers for international transport. These receipts include any other prepayment made for goods or services received in the destination country. They also may include receipts from same-day visitors, except when these are important enough to justify separate classification. For some countries they do not include receipts for passenger transport items. Data are in current U.S. dollars. |
| Military expenditure (current USD)                           | float   | 0 - 7.340000e+11             | Military expenditures data from SIPRI are derived from the NATO definition, which includes all current and capital expenditures on the armed forces, including peacekeeping forces; defense ministries and other government agencies engaged in defense projects; paramilitary forces, if these are judged to be trained and equipped for military operations; and military space activities. |
| Population growth (annual percent)                           | float   | -1.718541 - 4.921024         | Annual population growth rate for year t is the exponential rate of growth of midyear population from year t-1 to t, expressed as a percentage . Population is based on the de facto definition of population, which counts all residents regardless of legal status or citizenship. |
| Prevalence of undernourishment (percent of population)       | float   | 2.500000 - 48.000000         | Prevalence of undernourishments is the percentage of the population whose habitual food consumption is insufficient to provide the dietary energy levels that are required to maintain a normal active and healthy life. Data showing as 2.5 may signify a prevalence of undernourishment below 2.5%. |
| Refugee population by country or territory of asylum         | float   | 5 - 3.681688e+06             | Refugees are people who are recognized as refugees under the 1951 Convention Relating to the Status of Refugees or its 1967 Protocol, the 1969 Organization of African Unity Convention Governing the Specific Aspects of Refugee Problems in Africa, people recognized as refugees in accordance with the UNHCR statute, people granted refugee-like humanitarian status, and people provided temporary protection. |
| Strength of legal rights index (0=weak to 12=strong)         | int     | 0 - 12                       | Strength of legal rights index measures the degree to which collateral and bankruptcy laws protect the rights of borrowers and lenders and thus facilitate lending. The index ranges from 0 to 12, with higher scores indicating that these laws are better designed to expand access to credit. |
| Unemployment, total (percent of total labor force) (modeled ILO estimate) | float   | 0.1 - 28.469999              | Unemployment refers to the share of the labor force that is without work but available for and seeking employment. |
| Net official flows from UN agencies: Total                   | float   | 0 - 4.087526e+08             | Net official flows from UN agencies are the net disbursements of total official flows from the UN agencies. Total official flows are the sum of Official Development Assistance (ODA) or official aid and Other Official Flows (OOF) and represent the total disbursements by the official sector at large to the recipient country. |

### Files

This project and its accompanying data are stored in the following [git repository](https://git.generalassemb.ly/powersjv/project-group-project-4), and has the following structure:

- README file
- code
  - 01_data cleaning
  - 02_EDA
  - 03_Models
  - 04_Predictions
- data 
- images

## Analysis
---

After data cleaning and exploratory data analysis, [analysis](https://git.generalassemb.ly/powersjv/project-group-project-4/blob/2a91a3fd3a514b56c4f846851a24a72289caaa84/code/03_Models/03_Regression_Models_no_GNI.ipynb) was done for the following regression models to predict Annual GDP Percentage Change:


1. Linear Regression
2. KNN Regressor
3. Decision Tree Regressor
4. Random Forest Regressor
5. Adaboost regressor
6. Lasso
7. Ridge

The baseline model, the mean Annual GDP Percentage change, produced a Root Mean Squared Error of 2.46%.  The root mean squared error indiactes that the errors are about 2.46% off from the actual GDP Annual Percentage Change.  

We were able to predict the 2022 Annual GDP Percentage Change for the countries affected heavily by Ukrainian refugees. It remains to be seen how accurate this is as more refugees accumulate and as new data is used for predictions. For our predictions, refugee numbers from March 22, 2022 were used as well as imputed mean or median values for the missing economic features. 


## Conclusions
---
This project uses United  Nations data to provide an initial exploration of how human refugee flows may impact the economies of host nations. 

After comparing and tuning the models, Random Forest was deemed the best fit as it produce a smaller Root Mean Squared error of 2.15% for the test data. Additionally, the model can explain 38.65% of the variance in our target, which is better than the baseline model.

While we are confident in our model, we recognize the limitations with our data and time constraints. To move forward with a more accurate model, we would acquire more data and perform a deeper dive. We would also utilize a time series model to examine the impact past and present refugee flows have on future GDP growth.


## Recommendations
---

Data availability was uneven amongst countries and features of interest, forcing us to drop features and countries to perform methodologically robust analysis. If we could obtain data either for a longer time frame, greater number features and/or countries captured in this study, it would likely result in more detailed and generalizable results. 

- Explore a longer time horizon. The economic role refugees play in their host nation depends heavily on how long they remain in that country, from imposing costs in the near-term to providing increasing economic contributions over the long term. Therefore the time horizon of refugee flows is critical to analysis of their impact on a particular economy ([Kulhman 1990](https://econpapers.repec.org/RePEc:vua:wpaper:1990-35)).

- Additional features we believe could be valuable in analyzing refugee economic impact include wealth inequality, unemployment rate by demographic group, life expectancy, mortality, poverty, literacy, education, consumption, and living standards. With additional time and energy to collect these data, we could potentially expand our analysis to incorporate some, or most, of these features. 


- Increase the number of explored countries. 



 
