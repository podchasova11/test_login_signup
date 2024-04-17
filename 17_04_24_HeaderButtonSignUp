"""
-*- coding: utf-8 -*-
@Time    : 2023/04/17 21:30
@Author  : Mila Podchasova
"""
from datetime import datetime
import pytest
import allure
from pages.Signup_login.signup_login import SignupLogin
from pages.base_page import BasePage
from pages.Markets.markets_locators import HeaderElementLocators
from selenium.common.exceptions import ElementClickInterceptedException


class HeaderButtonSignUp(BasePage):

    def arrange_(self, cur_role, cur_item_link):
        print(f"\n{datetime.now()}   1. Arrange")

        if cur_role == "Auth":
            pytest.skip('This test not for "Auth" role')

        if not self.current_page_is(cur_item_link):
            self.link = cur_item_link
            self.open_page()

        print(f"{datetime.now()}   Is visible BUTTON_SIGNUP? =>")
        if self.element_is_visible(HeaderElementLocators.BUTTON_SIGNUP):
            print(f"{datetime.now()}   => BUTTON_SIGNUP is visible on the page!")
        else:
            print(f"{datetime.now()}   => BUTTON_SIGNUP is not visible on the page!")
            pytest.skip("Checking element is not on this page")

    @allure.step("Click [Sign Up] button")
    def element_click(self):
        print(f"\n{datetime.now()}   2. Act")
        print(f"{datetime.now()}   Start Click button [Sign Up] =>")
        button_list = self.driver.find_elements(*HeaderElementLocators.BUTTON_SIGNUP)
        if len(button_list) == 0:
            print(f"{datetime.now()}   => BUTTON_SIGNUP is not present on the page!")
            del button_list
            return False

        print(f"{datetime.now()}   BUTTON_SIGNUP scroll =>")
        self.driver.execute_script(
            'return arguments[0].scrollIntoView({block: "center", inline: "nearest"});',
            button_list[0]
        )

        print(f"{datetime.now()}   Is BUTTON_SIGNUP clickable? =>")
        if not self.element_is_clickable(button_list[0], 5):
            print(f"{datetime.now()}   => BUTTON_SIGNUP is not clickable")
            return False
        print(f"{datetime.now()}   => BUTTON_SIGNUP is clickable")

        print(f"{datetime.now()}   BUTTON_SIGNUP click =>")
        button_list = self.driver.find_elements(*HeaderElementLocators.BUTTON_SIGNUP)
        try:
            button_list[0].click()
            print(f"{datetime.now()}   => BUTTON_SIGNUP is clicked!")
        except ElementClickInterceptedException:
            print(f"{datetime.now()}   'Signup' or 'Login' form is automatically opened")

            page_ = SignupLogin(self.driver)
            if page_.close_signup_form():
                pass
            else:
                page_.close_signup_page()

            del page_
            button_list[0].click()

        del button_list
        return True
