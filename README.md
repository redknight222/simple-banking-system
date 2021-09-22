# simple-banking-system
This script creates bank card number and verifies the number using the Luna algorithm
import random


class Cards:

    data_cards = []

    def __init__(self):
        self.number = None
        self.pin = 0
        self.us_number = 0
        self.us_pin = 0
        self.q = 0

    def hello(self):
        print('1. Create an account\n2. Log into account\n0. Exit')
        i = int(input())
        if i == 0:
            print('\nBye!')
        elif i == 1:
            Cards.create_account(self)
        elif i == 2:
            Cards.log_account(self)
        else:
            pass

    def create_account(self):
        self.number = '400000' + ''.join([str(random.randint(0, 9)) for _ in range(9)])
        self.number = list(self.number)
        lun_num = [int(i) for i in self.number]
        for i in range(0, 16, 2):
            lun_num[i] = 2 * lun_num[i]
        lun_num = [i - 9 if i > 9 else i for i in lun_num]
        while True:
            q = random.randint(0, 9)
            if (sum(lun_num) + q) % 10 == 0:
                self.number.append(str(q))
                self.number = ''.join(self.number)
                break
            else:
                continue
        self.pin = ''.join([str(random.randint(0, 9)) for _ in range(4)])
        Cards.data_cards.append([self.number, self.pin])
        print(f'\nYour card has been created\nYour card number:\n{self.number}\nYour card PIN:\n{self.pin}\n')
        Cards.hello(self)

    def log_in(self):
        print('\n1. Balance\n2. Log out\n0. Exit')
        n = int(input())
        if n == 0:
            print('\nBye!')
        elif n == 1:
            print('\nBalance: 0')
            Cards.log_in(self)
        elif n == 2:
            print('\nYou have successfully logged out!\n')
            Cards.hello(self)
        else:
            pass

    def log_account(self):
        self.us_number = input('\nEnter your card number:\n')
        self.us_pin = input('Enter your PIN:\n')
        for self.m in Cards.data_cards:
            if self.us_number == self.m[0]:
                if self.us_pin == self.m[1]:
                    print('\nYou have successfully logged in!')
                    Cards.log_in(self)
                else:
                    print('\nWrong card number or PIN!\n')
                    Cards.hello(self)
            else:
                print('\nWrong card number or PIN!\n')
                Cards.hello(self)


my_card = Cards()
my_card.hello()
