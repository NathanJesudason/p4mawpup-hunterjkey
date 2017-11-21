These are other Webscraper things that I tried, it's just a record to refer to in the event that I'd like to try to fix any of these.

def Splinter():
	# open a browser
	
	browser = Browser('chrome')

	# Width, Height
	browser.driver.set_window_size(640, 480)
	
	browser.visit(lnk)

	search_results_xpath = '//h3[@class="r"]/a'
	search_results = browser.find_by_xpath(search_results_xpath)  # returns list of link elements

	# iterate through list of link elements
	scraped_data = []
	for search_result in search_results:

		title = search_result.text.encode('utf8')  # trust me, clean data
		link = search_result["href"]
		scraped_data.append((title, link))

	# put all the data into a pandas dataframe
	df = pd.DataFrame(data=scraped_data, columns=["title", "link"])
	df.to_csv("links.csv")	# export to csv

def lxml():
	"""
	page = requests.get(str(lnk))
	tree = html.fromstring(page.content)
	htmlElem = html.document_fromstring(sourceCode)
	
	
	#This will create a list of buyers:
	div = tree.xpath('//span[@id="yui_3_17_2_1_1511033227506_38"]/text()')
	print div
	"""
	headers= {"User-Agent":"Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.82 Safari/537.36"}
	page = requests.get(lnk
                    , headers=headers)
	tree = html.fromstring(page.content)
	assignment_name = tree.xpath('//a[@class="ac-algo fz-l ac-21th lh-24"]/text()')

	print(assignment_name)