## Running the Program

Clone or download the repo files and once you are in the root directory run:

```
npm install
npm start
```

Navigate to localhost:8080 and you can start to interact with your new virtual bank account. But make sure you initialise the account object first, in the example below I have created my own local 'account' with the following commands:

```
const account = new constructionModule.BankAccount();
account.addMoney(amount);
account.withdrawMoney(amount);
account.printStatement;
```

## Running the tests

Make sure you have ESlint and Karma functioning locally to see the coverage and test the code quality in your terminal:

```
npm install

```
To run the tests enter:

```
npm test
npx eslint <filename>
karma start
```

## Example Criteria:

Given a client makes a deposit of 1000 on 10-01-2012
And a deposit of 2000 on 13-01-2012
And a withdrawal of 500 on 14-01-2012
When she prints her bank statement
Then she would see

```
| date || credit || debit || balance |
| 14/01/2012 || || 500.00 || 2500.00 |
| 13/01/2012 || 2000.00 || || 3000.00 |
| 10/01/2012 || 1000.00 || || 1000.00 |
```

## The Process

* Setup - initialising a git, setting up my jasmine test suite and linter
* Planning - modelling the objects and the possible solutions for our requirements
* Feature Test - writing the first feature test for initial behaviour
* Unit Test - to check each object operates independently of another and reports the expected behaviour
* Red, Green, Refactor - write these failing tests, pass them with the simplest solution and then tidy up the code. Repeat.

## Plan and Model

To start with I began to think about all of the things this bank account would need to be able to do:

• Track the total amount of money (balance) • Increase the total when a deposit is made • Decrease the total when a withdrawal is made • Track the dates and transaction history • Output a formatted statement of the account's transaction history

| Object     | State         | Behaviour |
| ------------- |:-------------:| -----:|
| BankAccount | balance, Statement | addMoney(x), withdrawMoney(x), printStatement  |
| Transaction | total_amount, created_at, credit?, value |  |
| Statement | transactions = []; | format() |

BankAccount Class
 • Responsible for tracking and printing the transactions to the user

Transaction Class
 • Responsible for keeping track of when it was initialised, if it was a credit or debit transaction and the amount that was added or subtracted during the transaction

 Statement Class
 • Responsible for formatting the account summary to the user

This rough outline has a class BankAccount which oversees the implementation of 2 other classes, Transaction and Statement. Transaction objects are created any time money is added or withdrawn from the account and they track when and how much was moved. Statement objects fetch transaction objects and format them so the BankAccount can render a formatted response to the user.

## Assumptions

There were several assumptions that I based my tests and my solution around:

* A user will input whole numbers
* A user could enter information on multiple dates
