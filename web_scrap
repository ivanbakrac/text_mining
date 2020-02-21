import re
import time

import requests
from bs4 import BeautifulSoup


def web_scrap(url):
    for i in range(2):  # try 2 times and if does not work raise exception
        text_scrap = (
            []
        )  # create a empty list to be updated with text, we will append name and purpose
        try:
            for response in range(50):
                response = requests.get(url)
                soup = BeautifulSoup(response.text)  # parse html
                soup_text = soup.get_text()
                soup_text = soup_text.strip(" ").strip()
                extract_name = re.findall(
                    r"Name.+", soup_text
                )  # find words that begin with "Name"
                extract_purpose = re.findall(
                    r"Purpose.+", soup_text
                )  # find words that begin with "Purpose"
                extract_all = extract_name + extract_purpose  # sum up the strings
                text_scrap.append(extract_all)  # append name and purpose in the list
            with open("text_scrap.txt", "w") as f:
                f.write(str(text_scrap))
                f.close()
        except Exception:
            print("failed attempt", i)
            time.sleep(2)


url = "http://18.207.92.139:8000/random_company"
if __name__ == "__main__":
    web_scrap(url)

# test: print text file
file = open("text_scrap.txt", "r")
for line in file:
    line = line.rstrip()
    print(line)
