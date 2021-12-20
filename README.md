# DataScrapping-2
#USING OBJECT ORIENTED PROGRAMMING (OOP) FOR WEB SCRAPING

from bs4 import BeautifulSoup
import requests


class Scrapping:
    def __init__(self, job_title, location, page_num=1):
        self.job_title = job_title
        self.location = location
        self.page_number = page_num

        self.job_title = []
        self.location = []
        self.page_number = []
        self.date = []
        self.HEADERS = ({'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.61 Safari/537.36',
                        'Accept-Language': 'en-US, en;q=0.5'})

        self.response = requests.get(f'https://www.indeed.com/jobs?q={self.job_title}&l={self.location}', headers= self.HEADERS)
        self.soup = BeautifulSoup(self.response.text, 'html.parser')
        #print(self.soup.prettify())



    def jobs(self):
        jobs_elem = self.soup.find_all('div', {'class':'slider_container'})
        # print(jobs_elem)
        for job in jobs_elem:
            job_title = job.find('h2', {'class':'jobTitle'}).text.rstrip('\n')
            company = job.find('span', {'class':'companyName'}).text.rstrip('\n')
            job_description = job.find('div', {'class':'job-snippet'}).text.rstrip('\n')
            date = job.find('span', {'class':'date'}).text.rstrip('\n')

            self.job_title.append(job_title)
            self.company.append(company)
            self.job_description.append(job_description)
            self.date.append(date)
            print(job_title)


pythonquest = Scrapping('System Analyst', 'Chicago')
print(pythonquest.jobs())
