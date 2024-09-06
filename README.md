# fetching-data-using-webscraping
To create a  table present in a website by fetching data from it using webscraping in python
website url='https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'


code
webpage=requests.get('https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue')
soup=BeautifulSoup(webpage.text,'html')
table=soup.find('table',class_="wikitable sortable") //Extract table
table

th=table.find_all('th') //Extract tableheading
colheading=[]  //columns heading row
for i in th:
    colheading.append(i.text.strip())
colheading

tr=table.find_all('tr') //Extract tablerow
tr
trl=[]
for i in tr:
    trl.append(i.find_all('td'))
trl

df=pd.DataFrame(columns=colheading) //create dataframe with 1 row as columns heading
df

**Below code appends every extracted row into dataframe df**
rowlist=[]
for i in tr[1:]:
    row=i.find_all('td')
    individual_row_data=[data.text.strip() for data in row]
    rowlist.append(individual_row_data)
    length=len(df)
    df.loc[length]=individual_row_data   #for each row length is incremented intiallt it was 1 when colheadings were present

df-----The final Table
