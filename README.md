# simple-scraping-project
Scraping from wuzzuf site 
we will serarch in wuzzuf website for jobs such as python
1
import requests as r
2
from bs4 import BeautifulSoup
3
import pandas as pd
1
url='https://wuzzuf.net/search/jobs/?q=python&a=hpb'
2
page1=r.get(url)
3
page1
<Response [200]>
1
soup=BeautifulSoup(page1.content)
2
​
1
# jobs titles
job_title=soup.find_all('h2',{'class':'css-m604qf'})
jobs=[job.text for job in job_title]
1
job_title=soup.find_all('h2',{'class':'css-m604qf'})
2
jobs=[job.text for job in job_title]
3
jobs
['Senior Python Engineer',
 'Python Tech Lead',
 'Senior Software Engineer - Python',
 'Senior Backend (Python) Engineer - Customer Domain',
 'Experienced Python/Django Developer',
 'Python Full Stack Developer',
 'Python Backend Developer (Remote-First)',
 'Python Developer',
 'Python API Developer Ocucon Team (UK) - (Alexandria)',
 'Python Back End Developer',
 'Python / Django Senior Developer',
 'Senior Python Developer',
 'Python Developer Remote - Urgent',
 'Technical Team Leader - Python /Django',
 'Full Stack Developer (Vue Js, Python / Java)']
1
companies_names=soup.find_all('a',{'class':'css-17s97q8'})
2
company=[comp.text.replace('-','') for comp in companies_names]
3
company
['Brainology ',
 'Eastern Enterprise ',
 'Paymob Solutions ',
 'Nana ',
 'Infoblink ',
 'Luftborn ',
 'Estafsar ',
 'Trufla ',
 'Procrew ',
 'TA telecom ',
 'RDI ',
 'Andela ',
 'GetTechForce.com ',
 'Div Systems ',
 'SSC Egypt ']
1
# location
1
locations_names=soup.find_all('span',{'class':'css-5wys0k'})
['Cairo, Egypt ',
 'Cairo, Egypt ',
 'Maadi, Cairo, Egypt ',
 'Sheraton, Cairo, Egypt ',
 'Dokki, Giza, Egypt ',
 'Heliopolis, Cairo, Egypt ',
 'Downtown, Cairo, Egypt ',
 'Heliopolis, Cairo, Egypt ',
 'Alexandria, Egypt ',
 'Cairo, Egypt ',
 'Dokki, Giza, Egypt ',
 'Cairo, Egypt ',
 'Cairo, Egypt ',
 'Mokattam, Cairo, Egypt ',
 'Cairo, Egypt ']
df
1
dic={'job':jobs,'company':company,'location':locations}
2
df=pd.DataFrame(dic)
3
df
job	company	location
0	Senior Python Engineer	Brainology	Cairo, Egypt
1	Python Tech Lead	Eastern Enterprise	Cairo, Egypt
2	Senior Software Engineer - Python	Paymob Solutions	Maadi, Cairo, Egypt
3	Senior Backend (Python) Engineer - Customer Do...	Nana	Sheraton, Cairo, Egypt
4	Experienced Python/Django Developer	Infoblink	Dokki, Giza, Egypt
5	Python Full Stack Developer	Luftborn	Heliopolis, Cairo, Egypt
6	Python Backend Developer (Remote-First)	Estafsar	Downtown, Cairo, Egypt
7	Python Developer	Trufla	Heliopolis, Cairo, Egypt
8	Python API Developer Ocucon Team (UK) - (Alexa...	Procrew	Alexandria, Egypt
9	Python Back End Developer	TA telecom	Cairo, Egypt
10	Python / Django Senior Developer	RDI	Dokki, Giza, Egypt
11	Senior Python Developer	Andela	Cairo, Egypt
12	Python Developer Remote - Urgent	GetTechForce.com	Cairo, Egypt
13	Technical Team Leader - Python /Django	Div Systems	Mokattam, Cairo, Egypt
14	Full Stack Developer (Vue Js, Python / Java)	SSC Egypt	Cairo, Egypt
