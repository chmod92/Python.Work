from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from webdriver_manager.chrome import ChromeDriverManager
import time
import config

chrome_options = Options()
chrome_options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36')

#chrome_options.add_argument("--headless")

browser = webdriver.Chrome(ChromeDriverManager().install(),options=chrome_options)


def main():
    log_in()
    time.sleep(8)
    enter_timesheet()
    browser.implicitly_wait(8)
    clear_timesheet()
    fill_Timesheet()
    browser.quit()
    


def log_in():
    browser.get('https://time.roberthalf.com/psp/hrfsprd/EMPLOYEE/HRMS/s/WEBLIB_RH_TCAST.NAV_FUNCTIONS.FieldFormula.IScript_Navigation?FolderPath=PORTAL_ROOT_OBJECT.RH_TCAST.RH_TC_CA_CL_ACCESS&amp;languageCd=ENG')
    time.sleep(3)
    browser.implicitly_wait(20)
    username = browser.find_element_by_xpath(
        '//*[@id="j_id0:j_id20:j_id21:LOBloginform:username"]')
    password = browser.find_element_by_xpath(
        '//*[@id="j_id0:j_id20:j_id21:LOBloginform:password"]')
    button = browser.find_element_by_xpath(
        '//*[@id="j_id0:j_id20:j_id21:LOBloginform:j_id51"]')

    username.send_keys(config.un)
    time.sleep(.2)
    password.send_keys(config.pw)
    time.sleep(.3)
    button.click()
    time.sleep(3)
    browser.get('https://authorizeme.roberthalf.com/RHExtCommunityLandingPage?a=RH&c=US&d=en_US&language=en_US')


def enter_timesheet():
    browser.switch_to.frame(browser.find_element_by_tag_name("iframe"))
    browser.find_element_by_name('RH_TC_DERIVED_RH_TS_LINK').click()


def clear_timesheet():
    time.sleep(3)

    for col in range(1, 5):
        for box in range(2, 7):
            id = ('//*[@id="RH_PCH_TIME_{}${}"]'.format(col, box))
            browser.find_element_by_xpath(id).clear()

    # Save as draft

    browser.find_element_by_xpath(
        '//*[@id="RH_TC_DERIVED2_RH_BUTTON1"]').click()

    print('previous time has been cleared and saved as a draft')


def fill_Timesheet():
    time.sleep(3)
    # browser.switch_to.frame(browser.find_element_by_tag_name("iframe"))

    t_in = '8'
    t_out = '17'

    for box in range(2, 7):
        time_in = ('//*[@id="RH_PCH_TIME_1${}"]'.format(box))
        time_out = ('//*[@id="RH_PCH_TIME_4${}"]'.format(box))
        browser.find_element_by_xpath(time_in).send_keys(t_in)
        browser.find_element_by_xpath(time_out).send_keys(t_out)

    # Lunch out

    for box in range(2,7):
        browser.find_element_by_xpath('//*[@id="RH_PCH_TIME_2${}"]'.format(box)).send_keys('13')

    # Lunch in

    for box in range(2,7):
        browser.find_element_by_xpath('//*[@id="RH_PCH_TIME_3${}"]'.format(box)).send_keys('14')

    # Save as draft

    browser.find_element_by_xpath(
        '//*[@id="RH_TC_DERIVED2_RH_BUTTON1"]').click()


    print('Hours have been entered and saved as a draft')


main()
